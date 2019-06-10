# installgitbook

This guide is built based on https://gldraphael.com/blog/publishing-gitbook-to-github-pages/. It is tested for the bionic release of Ubuntu. This is giving instructions starting with a fresh installation of Ubuntu Bionic.


## Ubuntu bionic modules install

Install the following ubuntu packages:

```
apt update
apt install -y build-essential curl
curl -sL https://deb.nodesource.com/setup_10.x | bash -
apt install -y nodejs git
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
gitbook serve
```

Copy paste the address http://localhost:4000 in your browser.

