```
 _  _  _  _  _
(_)(_)(_)(_)(_)
          _(_)_         _   _  _  _  _    _  _  _  _  _       _  _
        _(_) (_)       (_) (_)(_)(_)(_)_ (_)(_)(_)(_)(_)_  _ (_)(_)
      _(_)   (_)       (_) (_)        (_(_) _  _  _ (_)(_)(_)
    _(_)     (_)       (_) (_)        (_(_)(_)(_)(_)(_)(_)
 _ (_) _  _  (_)_  _  _(_)_(_) _  _  _(_(_)_  _  _  _  (_)
(_)(_)(_)(_)(_)(_)(_)(_) (_(_)(_)(_)(_)   (_)(_)(_)(_) (_)
                           (_)
                           (_)
```

**Z**sh **U**ltimate **P**rogrammer's **E**xtensions **R**efurbished - version 0.1

# Introduction

Zuper is a minimalist library of extensions for Zsh programming,
because believe it or not Zsh is so slick and powerful that it can be
used as a programming language.

# Features

 - key/value store on files mapped to associative arrays
 - consul k/v integration using native get/set over ztcp
 - nifty messaging using colors and intl support (gettext)
 - procedural flow debugging functions and variable monitor
 - clean exit and destructors registration
 - improved temp file handling
 - more to come...

# Usage

Documentation is still lacking, however to use Zuper in Zsh scripts
one must first source its main library `zuper`, then declare global
variables and arrays, then source `zuper.init` and at the end of the
program call `endgame` for a clean exit. Example test program:

```zsh
#!/usr/bin/env zsh

# switch on debugging output
debug=1
# switch on zuper's key/value load/save extension
zkv=1
# switch off zuper's consul kv get/set extension
unset consul

source zuper

# declare a custom global variable
vars+=(myvar)
# assign a default value to our global variable
myvar=${myvar:-ok}

# declare a custom function to print it out
testfun() {
    # register the function in the debug flow
    fn "testfun"
    # print out with nice green colors
    notice "Custom var: $myvar"
}

# wrap the init phase
source zuper.init

# register the zdump debug function to be executed on exit
destruens+=(zdump)

# call our custom function
testfun

# declare an associative array map
typeset -A mymap
# we use words and their md5
mymap=(
    lorem f737a087bca81f69a6048ec744c73e41
    ipsum 02063b9bf9d6e15ad61226fa4584aae0
    dolor 5f20730ddc7a1fedbf265358f0ce4f26
)

# save the map into a file
zkv.save mymap test.map

# free the map
mymap=()

# re-declare the map
typeset -A mymap
# re-load saved contents
zkv.load test.map
# dump contents
for i in ${(k)mymap}; do
    print "$i \t ${mymap[$i]}"
done

# end the program (call destructors)
endgame
```


# Deployment

 - Devuan Simple Development Toolkit https://git.devuan.org/devuan/devuan-sdk#tab-readme
 - Dowse IoT awareness OS http://dyne.org/software/dowse
 - Jaro Mail terminal email http://dyne.org/software/jaro-mail

If you use it, let us know! http://dyne.org/contact

# License

Zuper is designed, developed and maintained by Denis Roio <jaromil@dyne.org>

Zuper is Copyright (C) 2015 by the Dyne.org foundation

This source code is free software; you can redistribute it and/or
modify it under the terms of the GNU Public License as published by
the Free Software Foundation; either version 3 of the License, or (at
your option) any later version.

This source code is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  Please refer to
the GNU Public License for more details.

You should have received a copy of the GNU Public License along with
this source code; if not, write to: Free Software Foundation, Inc.,
675 Mass Ave, Cambridge, MA 02139, USA.
