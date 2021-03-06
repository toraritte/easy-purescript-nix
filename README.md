# Easy PureScript Nix, NixOS Ready™

A project for using PureScript and related tooling easily with Nix. Note that the `purescript` derivation used in nixpkgs is a derivative of the derivatifrom this project, so if you do not care about which version of PureScript you want to use, you can simply use it from there.

## Example usage

See [ci.nix](./ci.nix) in this repo for example `nix-shell` usage.

## Potential questions

### How do I install to my system from here?

Behold:

```
> nix-env -f default.nix -iA purs
# or nix-env -if purs.nix

> which purs
/home/justin/.nix-profile/bin/purs
> purs --version
0.13.8
```

Or by `shell.nix`:

```nix
{ pkgs ? import <nixpkgs> { } }:
let
  easy-ps = import
    (pkgs.fetchFromGitHub {
      owner = "justinwoo";
      repo = "easy-purescript-nix";
      rev = "a5fd0328827ac46954db08f624c09eba981f1ab2";
      sha256 = "1g3bk2y8hz0y998yixz3jmvh553kjpj2k7j0xrp4al1jrbdcmgjq";
    }) {
    inherit pkgs;
  };
in
pkgs.mkShell {
  buildInputs = [
    easy-ps.purs-0_13_8
    easy-ps.psc-package
  ];
}
```

## Why was this made?

See the blog post about this here: <https://github.com/justinwoo/my-blog-posts/blob/master/posts/2018-10-24-using-purescript-easily-with-nix.md>

Raison d'etre: <https://github.com/justinwoo/my-blog-posts/blob/master/posts/2019-04-29-why-easy-purescript-nix.md>

## Credits

Thanks to Pekka (@kaitanie) for making this work on NixOS.
