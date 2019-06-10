# installgitbook

This guide is built based on https://gldraphael.com/blog/publishing-gitbook-to-github-pages/. It is tested for the bionic release of Ubuntu. This is giving instructions starting with a fresh installation of Ubuntu Bionic.


## Ubuntu bionic modules install

Install the following ubuntu packages:

```
apt update
apt install -y build-essential curl
curl -sL https://deb.nodesource.com/setup_10.x | bash -
apt install -y nodejs git emacs
```

## Install and initialize gitbook

```
npm install -g gitbook-cli
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
