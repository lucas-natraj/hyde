---
layout: post
category : web
author: Lucas Natraj
tags: [quick, tutorial]
title: Quick HTTP Server for Serving Static Content
---

*The following commands will start an http server for serving static content from the current (or specified) folder.*

### Node.js (http-server)

```bash
$ npm install -g http-server
$ http-server -p 8000
```

### Node.js (node-static)

```bash
$ npm install -g node-static
$ static -p 8000
```

### Python 2.x

```bash
$ python -m SimpleHTTPServer 8000
```

### Python 3.x

```bash
$ python -m http.server 8000
```

### Ruby (adsf - A Dead Simple Fileserver)

```bash
$ gem install adsf
$ adsf -p 8000
```
