# Change Log

### 0.0.16

* Add highlighting for `FUNCTION`

### 0.0.15

* Add highlighting for `SET`, `LET`, `ADD`, `STOP`, `SIGNAL`, `ONBUILD`, `SHELL`
* Add highlighting for command arguments such as `--required`
* Update so that earthly/earthfile-grammar is the single source of truth

### 0.0.14

* Fix documentation

### 0.0.13

* Add highlighting for `WAIT`, `TRY`, `FINALLY`, `CACHE`, `HOST`, `PIPELINE`, `TRIGGER` and `PROJECT`.

### 0.0.12

* Fix don't allow `-` in variable names.
* Fix arg names containing `_`

### 0.0.11

* Add highlighting for `FOR` and `VERSION`.
* Fix missing highlight for port number when space after EXPOSE has more than 1 space.

### 0.0.10

* Add highlighting for `DO`, `COMMAND`, `IMPORT` and `LOCALLY`.
* Add highlighting for command definition and references.
* Change the semantic type of targets to "class".

### 0.0.9

* Add highlighting for `IF`.

### 0.0.8

* Properly handle comments in conjunction with line continuation.

### 0.0.7

* Fix README image.

### 0.0.6

* Fix quote escaping.

### 0.0.5

* Fix `FROM DOCKERFILE`
* Fix highlighting for target and artifact refs in edge cases (eg `g++`)
* Make case-sensitive
* Add highlighting for `WITH DOCKER` ... `END`

### 0.0.4

* Add highlighting for `FROM DOCKERFILE`

### 0.0.3

* Add highlighting for `HEALTHCHECK`.
* Switch from `build.earth` to `Earthfile`.

### 0.0.2

Add screenshot in the README.

### 0.0.1

Initial release of earthfile-syntax-highlighting.
