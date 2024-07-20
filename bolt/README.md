### Development

When building these Rust modules, the will compile to `.so` files with a `lib`
prefix. Create symbolic links for the appropriate name, eg.
```sh
ln -s full/path/to/libbolt.so bolt.so
```
The same goes for the compiled emacs module mentioned below.

#### Emacs rs module

This module allows continuous loading and unloading of the dynamic module. This is
required because Emacs doesn't natively allow unloading already loaded modules.

Clone the `emacs-module-rs` [repo](https://github.com/ubolonton/emacs-module-rs),
compile the `rs-module` project, and add the compiled module's directory to `load-path`.

This will allow continues reloading of the module during development by doing the
following:

```elisp
(add-to-list 'load-path "<path to compiled rs-module>")
(rs-module/load "./target/debug/bolt.so")
```

On every subsequent recompilation of the module, execute `rs-module/load` again.
