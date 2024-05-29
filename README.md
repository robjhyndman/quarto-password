This is a skeleton quarto template for a website that is password protected and deployed on GitHub Pages.

The website is built and deployed on GitHub Actions.

To use, it fork or clone this site to a private GitHub repo, then do the following:

1. Go to `Settings/Pages` and find "Build and deployment" and set "Source" to "GitHub Pages".
2. The password is set in the following line from the [GitHub Action](.GitHub/workflows/quarto-gh-pages-html.yml):

   ```
         - run: staticrypt _site/* -r -d _site -p password --short
   ```

   * Change `password` to whatever you prefer to use.
   * Currently, the entire website is password protected. You could also just add a password to one folder in the website. To do that, replace `_site` with `_site/folder` (in both places).
