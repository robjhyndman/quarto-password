This is a skeleton quarto template for a website that is password protected and deployed on GitHub Pages.

The website is built and deployed on GitHub Actions.

The GitHub Action, `.github/workflows/quarto-gh-pages-html.yml` does the following:

- Installs R packages using renv
- Renders the project via `quarto render`
- adds password via `staticrypt`
- deploys to Github Pages (given correct configuration as per below)

## Use Template and Configure GitHub Pages Site Deployment

To use, it fork or clone this site to a private GitHub repo, then do the following:

1. Go to `Settings/Pages` and find "Build and deployment" and set "Source" to "GitHub Actions".
2. A little further down the page, check "Enforce HTTPS"
3. The password is set in the following line from the [GitHub Action](.github/workflows/quarto-gh-pages-html.yml):

   ```
         - run: staticrypt _site/* -r -d _site -p password --short
   ```

   * Change `password` to whatever you prefer to use.
   * Currently, the entire website is password protected. You could also just add a password to one folder in the website. To do that, replace `_site` with `_site/folder` (in both places).

## Adding encryption to existing Quarto Website

To add encryption to an existing website, simply:

1. Copy and paste `quarto-gh-pages-html.yml` into `.github/workflows/` your existing repo, creating the folder if it doesn't exist.
2. configure GitHub Pages to deploy from GitHub Actions as per instructions above.

## Modify Action to render Quarto Website without Computations

If you prefer to run your computations locally, you can use the [Freeze execution option](https://quarto.org/docs/projects/code-execution.html#freeze). Set `freeze: true` under `excute:` options in your `_quarto.yml` and remove/comment the `r-lib` steps in `.github/workflows/quarto-gh-pages-html.yml`.

See this gist for modified action: <https://gist.github.com/cynthiahqy/c53e6947b6da7364f9090f3d77b006d>.

To add the modified action to an existing repo (without any GitHub actions) using GitHub CLI:

```
gh gist clone https://gist.github.com/cynthiahqy/c53e6947b6da7364f9090f3d77b006df
mkdir .github
mv c53e6947b6da7364f9090f3d77b006df .github/workflows
```



