## Encrypted Static (Quarto) Website

This is a skeleton template for a [Quarto website](https://quarto.org/docs/websites/) that is password protected and deployed on GitHub Pages.

The website is built and deployed on GitHub Actions. It assumes any computations are run locally and tracked via the [Freeze execution option](https://quarto.org/docs/projects/code-execution.html#freeze) (i.e. `freeze: true` in `_quarto.yml`).

The GitHub Action, [`quarto-staticrypt-ghpages.yml`](.github/workflows/quarto-staticrypt-ghpages.yml) does the following:

- Renders the Quarto project via `quarto render`.
- Adds password via `staticrypt`
- deploys to Github Pages (given correct configuration as per below)

Use the "Use this template" button to create a new private GitHub repo with all the files in this repo.

## Configure password and protected pages

Modify website build and encryption settings in [`quarto-staticrypt-ghpages.yml`](.github/workflows/quarto-staticrypt-ghpages.yml) as necessary:
   ```
   build:
   ...
   env:
      PROTECTED_DIR: _site
      PASSWORD: password
      # PASSWORD: ${{ secrets.YOUR_SECRET }}
   ```

   * `PROTECTED_DIR` should match your Quarto project output directory, which by default is `output_dir: _site`.
      * To protect a folder of pages rather than your whole website, modify `_site` to `_site/folder`.
   * `PASSWORD` sets the encryption password for all pages in `PROTECTED_DIR`.
      * For simplicity, the password is specified by default in plain-text as shown. This means anyone who can access the repository can open this file and read the password. Therefore, make sure your repository remains PRIVATE.
      * A more secure option, with *slightly* more setup is to store the password in a [GitHub Secret](https://docs.github.com/en/actions/security-guides/using-secrets-in-github-actions). Follow these [instructions](https://docs.github.com/en/actions/security-guides/using-secrets-in-github-actions#creating-secrets-for-a-repository) to add secret repository variable that stores your password separately from the github action file. Make sure you comment/uncomment the relevant `PASSWORD:` line, and the name of your secret matches what's in the file (e.g. `YOUR_SECRET`)

## Configure GitHub Pages Site Deployment

1. Go to `Settings/Pages` and find "Build and deployment" and set "Source" to "GitHub Actions".
2. A little further down the page, check "Enforce HTTPS"

## Adding encryption to existing Quarto Website

To add encryption to an existing website, simply:

1. Copy and paste [`quarto-staticrypt-ghpages.yml`](.github/workflows/quarto-staticrypt-ghpages.yml) into `.github/workflows/` your existing repo, creating the folder if it doesn't exist.
2. configure GitHub Pages to deploy from GitHub Actions as per instructions above.

## Modify Action to run Computations before rendering Quarto Website.

If you want to run your computations on GitHub actions before rendering the website:

- uncomment the R code steps in the `build` job of [`quarto-staticrypt-ghpages.yml`](.github/workflows/quarto-staticrypt-ghpages.yml)
- [optional] change `freeze: true` to `auto` or `false` in [`_quarto.yml`](quarto.yml)
