# **Project Setup**

## **Get Started**

Start your laravel project by command-> `laravel new symposium`
Starter kit -> `Laravel Breeze`  
Breeze stack  -> `Blade with Alpine` 
Testing framework -> `Pest`  
Database  -> `Mysql`  

## **Install Duster**

Duster Repository-> https://github.com/tighten/duster
```bash
composer require tightenco/duster --dev
./vendor/bin/duster github-actions
./vendor/bin/duster husky-hooks
```
## **Install Prettier**

Install prettier -> `npm install --save-dev prettier-plugin-blade@^2 prettier prettier-plugin-tailwindcss`

Edit -> `vim .prettierrc`
```bash
{
  "printWidth": 120,
  "semi": true,
  "singleQuote": true,
  "tabWidth": 4,
  "trailingComma": "all",
  "plugins": ["prettier-plugin-blade", "prettier-plugin-tailwindcss"],
  "overrides": [
    {
      "files": [
        "*.blade.php"
      ],
      "options": {
        "parser": "blade"
      }
    }
  ]
}
```

Edit -> `vim .prettierignore`

```bash
node_modules
dist
.env*
vendor/
/vendor
public/
.git
**/.git
package-lock.json
composer.lock
```

Edit -> `vim lint-staged.config.js`

`'**/*': 'prettier --write --ignore-unknown'`

## **Run Prettier in GitHub Actions**

Blog link -> https://mskelton.medium.com/auto-formatting-code-using-prettier-and-github-actions-ed458f58b7df

gitgub/workflows -> create -> `prettier-write.yml`

```bash
name: Format
on:
  pull_request:
    branches: [main]
jobs:
  format:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
        with:
          ref: ${{ github.head_ref }}
      - uses: actions/setup-node@v2
        with:
          node-version: "14.x"
      - run: npm ci
      - run: npm run format
      - name: Commit changes
        uses: stefanzweifel/git-auto-commit-action@v4
        with:
          commit_message: Apply formatting changes
          branch: ${{ github.head_ref }}
```
