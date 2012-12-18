continuation.js
===============

Continuation support for Node.js

* It converts JavaScript code into Continuation Passing Style (CPS) code in a best effort manner.
* Fallback mechanism when CPS is not possible / not implemented.
* Tail calls are properly handled.
* Passing user-defined continuation is possible (but, it's not a pure continuation).

How to use
----------

### From github

    % git clone https://github.com/dai-shi/continuation.js.git
    % ./bin/continuation-compile sample/fact.js > cps_fact.js
    
    % node -e "console.log(require('./sample/fact.js').fact(100000))"
    
    .../continuation.js/sample/fact.js:2
      function fact_tail(x, r) {
                            ^
    RangeError: Maximum call stack size exceeded
    
    % node -e "console.log(require('./cps_fact.js').fact(100000))"
    Infinity

How it works
------------

* 4 classes are defined in the global scope.
    * CpsFunction
    * CpsContinuation
    * CpsResult
    * CpsRun
* CPS enabled functions have the CpsEnabled=true property.
* Traversing AST to transform into CPS, only when possible!
* Keeping original code so that non-CPS is always possible.

Limitations
-----------

* There are some overhead, obviously.
* Not all calls are transformed into CPS.
* Arguments objects are handled, but it may causes some problems.
* Maybe some more.

TODOs
-----

* Integrate with Node.js module system.
* Better documents.
* Transform non-tail calls into CPS.
* More tests.
* Avoid duplicating functions.
* Fix ugly code.

Author
------

Daishi Kato [@dai_shi](https://twitter.com/dai_shi)
