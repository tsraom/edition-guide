# Cargoでローカルのレジストリの使用が可能になりました
<!-- # Cargo can use a local registry replacement -->

<!-- ![Minimum Rust version: 1.12](https://img.shields.io/badge/Minimum%20Rust%20Version-1.12-brightgreen.svg) -->

![最低限必要Rustバージョン: 1.12](https://img.shields.io/badge/Minimum%20Rust%20Version-1.12-brightgreen.svg)

<!-- Cargo finds its packages in a "source". The default source is [crates.io](https://crates.io). However, you -->
<!-- can choose a different source in your `.cargo/config`: -->

Cargoは「ソース」の中でパッケージを見つけます。デフォルトのソースは
[crates.io](https://crates.io)です。`.cargo/config`で別のソースを指定することも
できます。

```toml
[source.crates-io]
replace-with = 'my-awesome-registry'

[source.my-awesome-registry]
registry = 'https://github.com/my-awesome/registry-index'
```

<!-- This configuration means that instead of using crates.io, Cargo will query -->
<!-- the `my-awesome-registry` source instead (configured to a different index -->
<!-- here). This alternate source *must be the exact same* as the crates.io index. -->
<!-- Cargo assumes that replacement sources are exact 1:1 mirrors in this respect, -->
<!-- and the following support is designed around that assumption. -->

この配置は、Rustがcrates.ioの代わりに(別のインデックスと指定された)
`my-awesome-registry`を問い合わせることを意味します。代わりとなるソースは、
`crates.io`と*全く同じ*でなければなりません。この点において、代わりとなるソース
が`crates.io`と完全に一対一のミラーであることをCargoは仮定します。

<!-- When generating a lock file for crate using a replacement registry, the -->
<!-- original registry will be encoded into the lock file. For example in the -->
<!-- configuration above, all lock files will still mention crates.io as the -->
<!-- registry that packages originated from. This semantically represents how -->
<!-- crates.io is the source of truth for all crates, and this is upheld because -->
<!-- all replacements have a 1:1 correspondance. -->

クレートのロックファイルが生成される時は、元のレジストリがロックファイルがロック
ファイル内に記録されます。例えば、上記の配置の元では、全てのロックファイルが
パッケージが由来するレジストリとして記録するのはやはりcrates.ioとなります。
これはcrates.ioが全てのクレートの本当の元であることを意味的に示します。代わりの
レジストリとcrates.ioの間に一対一の対応関係があるため、この記録方式は成り立つの
です。

<!-- Overall, this means that no matter what replacement source you're working -->
<!-- with, you can ship your lock file to anyone else and you'll all still have -->
<!-- verifiably reproducible builds! -->

総合的に言うと、つまり、あなたがcrates.ioの代わりに如何なるソースを使用していて
も、誰もがあなたのリリースしたロックファイルを使ってビルドを再現できるということ
です。

<!-- This has enabled tools like -->
<!-- [`cargo-vendor`](https://github.com/alexcrichton/cargo-vendor) and -->
<!-- [`cargo-local-registry`](https://github.com/alexcrichton/cargo-local-registry), -->
<!-- which are often useful for "offline builds." They prepare the list of all -->
<!-- Rust dependencies ahead of time, which lets you ship them to a build machine -->
<!-- with ease. -->

これによって、「オフラインビルド」を行うために便利なツールである
[`cargo-vendor`](https://github.com/alexcrichton/cargo-vendor)や
[`cargo-local-registry`](https://github.com/alexcrichton/cargo-local-registry)が
が実現可能になりました。これらのツールは、Rustの全ての依存性をあらかじめ用意し、
それらのビルドマシンへのリリースを容易にします。
