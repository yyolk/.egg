.egg
====

_Note: This is a work in progress / proof of concept._

Abstract
--------

`.egg` is an attempt to create a **digital artifact**. 

Data can of course be copied, so the idea of an artifact within the realm of data, a file that is copied, and loses integrity degrades that through corruption.

By referencing a single version or container for any production / expression of data requires the data be packaged if it contains multiple assets (much like a zip).

The second part is a checksum. Checksums are a quick an efficient way to compute a set-length piece of data that is unique depending on the data put in.

Often, this is done with `md5`.

`.egg` = `md5 checksum` + `.tar.gz`/`.bz2`/`.7z`/…
--------------------------------------------------

By sending a file in a `.egg` a simple bash script could compute the file, since the filename is simply the `md5` sum appended with `.egg` (instead of the extension of whatever archive type it is; multiple formats could be supported but would require a file-check of some-type or the addition of metadata.)

Bash script `doteggcheck.sh *.egg`

```bash
#!/usr/bin/env bash

md5 $1 | awk '{print $4}' | diff <(echo "`basename $1 .egg`") -
```



Workflow
--------

_will change, this is a generalized overview_

`dotegg` _will be_ a POSIX app and can be expected to work many ways and utilize Unix pipes and workflows.

`dotegg in.jpg` or `dotegg < in.jpg` or `cat in.jpg |dotegg`

`dotegg` will generate a new `.egg` file that will be output in the current working directory. 


The filename length of a `.egg` will always be 35 characters long. That is because the length of a `md5` sum is always 32 characters and we will always append `.egg` as well.

    in.jpg
    
becomes
    
    764efa883dda1e11db47671c4a3bbd9e.egg
