# Crates.ioはワイルドカードで指定された依存性を受け付けなくなりました
<!-- # Crates.io disallows wildcard dependencies -->

<!-- ![Minimum Rust version: 1.6](https://img.shields.io/badge/Minimum%20Rust%20Version-1.6-brightgreen.svg) -->

![最低限必要Rustバージョン: 1.6](https://img.shields.io/badge/Minimum%20Rust%20Version-1.6-brightgreen.svg)

<!-- Crates.io will not allow you to upload a package with a wildcard dependency. -->
<!-- In other words, these: -->

ワイルドカードで指定された依存性を含むパッケージはcrates.ioにアップロードする
ことはできません。つまり、下記のような依存性のことです。

```toml
[dependencies]
regex = "*"
```

<!-- A wildcard dependency means that you work with any possible version of your -->
<!-- dependency. This is highly unlikely to be true, and would cause unnecessary -->
<!-- breakage in the ecosystem. -->

依存性にワイルドカードを指定することは、依存先が如何なるバージョンでもあなたの
コードが動作することを保証するという意味です。これは、ほとんどの場合において
不可能であり、エコシステム内で無駄な破綻を引き起こします。

<!-- Instead, depend on a version range. For example, `^` is the default, so -->
<!-- you could use -->

依存性にはワイルドカードを使用せずに、バージョン範囲を指定してください。例えば、
`^`がデフォルトなので、下記のように依存性を指定することができます。

```toml
[dependencies]
regex = "1.0.0"
```

<!-- instead. `>`, `<=`, and all of the other, non-`*` ranges work as well. -->

`>`や`<=`、そして`*`ではないバージョン範囲は全て指定することができます。
