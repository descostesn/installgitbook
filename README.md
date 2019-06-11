# Create a gitbook from scratch and for free

This guide is built based on https://gldraphael.com/blog/publishing-gitbook-to-github-pages/. It is tested for the bionic release of Ubuntu. This is giving instructions starting with a fresh installation of Ubuntu Bionic.


## Ubuntu bionic modules install

Install the following ubuntu packages:

```
sudo apt update
sudo apt install -y build-essential curl
curl rl -sL https://deb.nodesource.com/setup_10.x | sudo bash -
sudo apt install -y nodejs git emacs
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
sudo apt update
sudo apt install -y --no-install-recommends yarn
sudo npm install -g gulp
```

## Install and initialize gitbook

```
sudo npm install -g gitbook-cli
git init gitbook-test
```
Enter folder and initialize:

```
cd gitbook-test
gitbook init
```
Update the content of README.md and SUMMARY.md and then visualize the gitbook on you local computer:

```
emacs README.md ## Press ctrl+X ctrl+S to save followed by ctrl+X ctrl+C to quit
emacs SUMMARY.md ## Press ctrl+X ctrl+S to save followed by ctrl+X ctrl+C to quit
gitbook serve
```

Copy paste the address http://localhost:4000 in your browser. Now create the .gitignore file:

```
emacs .gitignore ## Press ctrl+X ctrl+S to save followed by ctrl+X ctrl+C to quit
```

That should contain:

```
.grunt
node_modules
_book
*.epub
*.mobi
*.pdf
*~
```

## Sending book on github

Go to github and create a new repository gitbook-test. Then enter the following commands in your current folder (replacing my name and email every time you should):

```
git config --global user.email "nicolas.descostes@embl.it"
git config --global user.name "descostesn"
git init
git add .
git commit -m "first commit"
git remote add origin https://github.com/descostesn/gitbook-test.git ## replacing by your github username
git push -u origin master
```

To publish a Github site, you need to push the source files to a gh-pages branch.

```
git branch gh-pages
git checkout gh-pages
git push -u origin gh-pages
git checkout master
```

## Set up a gulp task to publish to GitHub Pages

If the command below does not work, try running it with sudo. Just press enter to all questions, this will create a package.json file and install dependencies:

```
yarn init  ## or 'sudo yarn init' if this does not work
yarn add gulp gulp-gh-pages gulp-load-plugins --dev
```

Create a new file called gulpfile.js and add the following code to it:

```
const gulp = require('gulp');
const gulpLoadPlugins = require('gulp-load-plugins');

const $ = gulpLoadPlugins();

// Publishes the site to GitHub Pages
gulp.task('publish', () => {
  console.log('Publishing to GH Pages');
  return gulp.src('./_book/**/*')
    .pipe($.ghPages({
      origin: 'origin',
      branch: 'gh-pages'
    }));
});
```

Now publish the website with:

```
gulp publish
```

My page is visible at  https://descostesn.github.io/gitbook-test/. You can either replace my username by yours or go to 'settings' and scroll down to see your address. 

After making modifications to your book, first commit and push the changes:

```
git add modifiedfile
git commit -m 'I have done a modification'
git push
```

Then:

```
gitbook build
gulp publish
```


