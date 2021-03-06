<div align="center">
    <a href="https://fl4m3ph03n1x.github.io/crossbarjs/index.html">
        <img src="./logos/logo_no_wm.png">
    </a>
</div>
<div align="center">

[![NPM](https://nodei.co/npm/crossbarjs.png?downloads=true&downloadRank=true&stars=true)](https://nodei.co/npm/crossbarjs/)

[![Build Status](https://travis-ci.org/Fl4m3Ph03n1x/crossbarjs.svg?branch=master)](https://travis-ci.org/Fl4m3Ph03n1x/crossbarjs) [![codecov](https://codecov.io/gh/Fl4m3Ph03n1x/crossbarjs/branch/master/graph/badge.svg)](https://codecov.io/gh/Fl4m3Ph03n1x/crossbarjs) [![Dependency Status](https://david-dm.org/Fl4m3Ph03n1x/crossbarjs.svg)](https://david-dm.org/Fl4m3Ph03n1x/crossbarjs) [![Code Climate](https://codeclimate.com/github/Fl4m3Ph03n1x/crossbarjs/badges/gpa.svg)](https://codeclimate.com/github/Fl4m3Ph03n1x/crossbarjs)
[![Known Vulnerabilities](https://snyk.io/test/github/fl4m3ph03n1x/crossbarjs/badge.svg)](https://snyk.io/test/github/fl4m3ph03n1x/crossbarjs)
[![contributions welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat)](https://github.com/Fl4m3Ph03n1x/crossbarjs/issues)

</div>

# What

`crossbarjs` is a library whose main purpose is to make interactions with crossbar easier, with support and focus over the 4 main crossbar functionalities and their counterparts:

 - publish
 - subscribe/unsubscribe
 - register/unregister
 - call

Without compromising access to any of the more advanced functionalities provided in the layer bellow.

# Why

 - `autobahn-js` (the only other option for JavaScript) API is long and it breaks the principle of [least astonishment](https://en.wikipedia.org/wiki/Principle_of_least_astonishment). To use it you need to go through pages of sparse documentation understand advanced principles of JavaScript. `crossbarjs` is an attempt at fixing that. The API it provides is as simple and beginner friendly as possible and its purpose is to make sure that all you need to run crossbario is to download this module and run it without spending extra time on docs, as it is designed to be as intuitive as possible. `crossbarjs` uses `autobahn-js` behind the hood, so you can have all the advanced features of the latter one without all of the hassle.

 - `crossbarjs` handles full automatic reconnection, unlike its competitor. With `crossbarjs` if your connection fails, the library will attempt a partial reconnect first and then will re-subscribe and re-register everything, so your service keeps working as expected with no down time whatsoever. Its like nothing happened at all.

# How

Following are instructions on how to install and use `crossbarjs`. For questions you can ask in the issues page:

 - [crossbarjs Issues](https://github.com/Fl4m3Ph03n1x/crossbarjs/issues)

For additional information on the API, feel free to check the [crossbarjs home page](https://fl4m3ph03n1x.github.io/crossbarjs/index.html).

## Install

Before using this module, you need to have crossbar installed and running. Then you can do:

    npm install crossbarjs --save

##  API

### Functions
 - <a href="https://fl4m3ph03n1x.github.io/crossbarjs/module-crossbarFacade.html#~connect__anchor">connect</a>
 - <a href="https://fl4m3ph03n1x.github.io/crossbarjs/module-crossbarFacade.html#~disconnect__anchor">disconnect</a>
 - <a href="https://fl4m3ph03n1x.github.io/crossbarjs/module-crossbarFacade.html#~getSession__anchor">getSession</a>
 - <a href="https://fl4m3ph03n1x.github.io/crossbarjs/module-crossbarFacade.html#~getConnection__anchor">getConnection</a>
 - <a href="https://fl4m3ph03n1x.github.io/crossbarjs/module-crossbarFacade.html#~register__anchor">register</a>
 - <a href="https://fl4m3ph03n1x.github.io/crossbarjs/module-crossbarFacade.html#~unregister__anchor">unregister</a>
 - <a href="https://fl4m3ph03n1x.github.io/crossbarjs/module-crossbarFacade.html#~call__anchor">call</a>
 - <a href="https://fl4m3ph03n1x.github.io/crossbarjs/module-crossbarFacade.html#~setOpts__anchor">setOpts</a>
 - <a href="https://fl4m3ph03n1x.github.io/crossbarjs/module-crossbarFacade.html#~getOpts__anchor">getOpts</a>
 - <a href="https://fl4m3ph03n1x.github.io/crossbarjs/module-crossbarFacade.html#~setOptsDefault__anchor">setOptsDefault</a>
 - <a href="https://fl4m3ph03n1x.github.io/crossbarjs/module-crossbarFacade.html#~publish__anchor">publish</a>
 - <a href="https://fl4m3ph03n1x.github.io/crossbarjs/module-crossbarFacade.html#~subscribe__anchor">subscribe</a>
 - <a href="https://fl4m3ph03n1x.github.io/crossbarjs/module-crossbarFacade.html#~unsubscribe__anchor">unsubscribe</a>

### Events

 - <a href="https://fl4m3ph03n1x.github.io/crossbarjs/module-crossbarFacade.html#~onClose__anchor">onClose</a>
 - <a href="https://fl4m3ph03n1x.github.io/crossbarjs/module-crossbarFacade.html#~onOpen__anchor">onOpen</a>
 - <a href="https://fl4m3ph03n1x.github.io/crossbarjs/module-crossbarFacade.html#~onError__anchor">onError</a>
 - <a href="https://fl4m3ph03n1x.github.io/crossbarjs/module-crossbarFacade.html#~onRecover__anchor">onRecover</a>

##  Examples

Connect and publish a message:

```
const crossbarjs = require("crossbarjs");

const crossbar  = crossbarjs();

crossbar.connect()
    .then(() => {
        crossbar.publish("myTopic", "arg1", "arg2");
    })
    .catch(console.log);
```

Subscribe to a topic:

```
const crossbarjs = require("crossbarjs");

const crossbar  = crossbarjs();

crossbar.connect()
    .then(() => {
        const print = (str1, str2) => console.log(`str1 is ${str1}, str2 is ${str2}`);
        return crossbar.subscribe("myTopic", print);
    })
    .catch(console.log);
```

Register a bunch of RPCs:

```
const crossbarjs = require("crossbarjs");

const crossbar  = crossbarjs();
    //after connecting
    const print = (str1, str2) => console.log(`str1 is ${str1}, str2 is ${str2}`);
    const add3 = (n1, n2, n3) => n1 + n2 + n3;

    crossbar.register([
        { "print": func: print },
        { "addThreeNumbers" : func: add3 }
    ])
    .then(() => console.log("Register successful"))
    .catch(console.log);
```

Unregister a bunch of RPCs:

```
//after connecting and registering
crossbar.unregister("print", "addThreeNumbers")
    .then(() => console.log("Unregister successful"))
    .catch(console.log);
```

Call an RPC:

```
    //after connecting and registering
    crossbar.call("addThreeNumbers", 1, 2, 3)
        .then(res => console.log(res))
        .catch(console.log);
```
