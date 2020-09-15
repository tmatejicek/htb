# htb.tomasmatejicek.cz

If you'd like to preview the web locally (for example, in the process of proposing a change):

1. Clone down the web's repository (`git clone https://github.com/tmatejicek/htb.tomasmatejicek.cz`)
2. `cd` into the web's directory
3. Run `bundle install` to install the necessary dependencies
4. Run `bundle exec jekyll serve` to start the preview server
5. Visit [`localhost:4000`](http://localhost:4000) in your browser to preview the web


### Deployment
```
rm -rf .git
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/tmatejicek/htb.tomasmatejicek.cz.git
git branch -D master
git branch -m gh-pages
git push -u --force origin gh-pages
```