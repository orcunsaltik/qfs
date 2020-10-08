# Node Js File System
[![Build Status](https://travis-ci.com/orcunsaltik/njfs.svg?branch=master)](https://travis-ci.com/orcunsaltik/njfs)
[![Dependency Status](https://david-dm.org/orcunsaltik/njfs.svg)](https://david-dm.org/orcunsaltik/njfs)
[![devDependencies Status](https://david-dm.org/orcunsaltik/njfs/dev-status.svg)](https://david-dm.org/orcunsaltik/njfs?type=dev)
[![Maintainability](https://api.codeclimate.com/v1/badges/035ff3499e767eb6b552/maintainability)](https://codeclimate.com/github/orcunsaltik/njfs/maintainability)
![Snyk Vulnerabilities for GitHub Repo](https://img.shields.io/snyk/vulnerabilities/github/orcunsaltik/njfs)
![npm](https://img.shields.io/npm/dt/njfs)
[![NPM Version](https://badge.fury.io/js/njfs.svg?style=flat)](https://npmjs.org/package/njfs)
[![contributions welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat)](https://github.com/orcunsaltik/njfs/issues)

A small collection of sync & async filesystem functions for Node Js. 

## Install

``` bash
npm install njfs
```

## Methods

1. unix(path): Synchronous. Returns path with unix-like directory separators.
2. root(path): Synchronous. Returns the root directory of the package.
3. list(path): Asynchronous. Returns the list of files and folders of the given path.
4. move(path, dest): Asynchronous. Moves files or folders.
5. copy(path, dest): Asynchronous. Copies files or folders.
6. isFile(path): Synchronous. Checks whether the specified path is an existing file or not.
7. isDir(path): Synchronous. Checks whether the specified path is an existing directory or not.

## Usage

``` js
const {move, copy, list, isDir} = require('njfs');

gulp.task('example', async () =>

    await gulp.watch(['./src/**/*.js'], gulp.series('build', async () => {

        const dist = 'vhosts/a';
        const dest = 'vhosts/a/b/c/js';

        try {
            const files = await list(dist);
            await Promise.all(files.map(async (file) => {
                const path = `${dist}/${file}`;
                if (!isDir(path)) {
                    await copy(path, dest);
                    console.log(`${file} transfered to ${dest}`);
                }
            }));
        } catch (e) {
            console.log(e);
        }
    })
));
```
