# Cargo

## Rust 项目使用 Cargo 管理

### 创建新项目

使用 `cargo new` 命令创建一个新的 Rust 项目：

```
$ cargo new hello_world
```

这将创建一个名为 `hello_world` 的新项目，其中包括一个 `Cargo.toml` 文件和一个 `src` 目录，其中包含一个 `main.rs` 文件。

### 添加依赖项

要添加一个依赖项，只需编辑 `Cargo.toml` 文件并添加所需的依赖项。例如，要添加一个名为 `rand` 的随机数生成器库，可以将以下行添加到 `Cargo.toml` 文件中的 `[dependencies]` 部分：

```toml
[dependencies]
rand = "0.8.4"
```

然后，运行 `cargo build` 命令，Cargo 将会自动下载并构建所需的依赖项。

### 构建项目

要构建项目，只需在项目根目录下运行 `cargo build` 命令：

```
$ cargo build
```

这将会编译项目并生成可执行文件。可执行文件在 `target/debug` 目录下生成。

### 运行项目

要运行项目，只需在项目根目录下运行 `cargo run` 命令：

```
$ cargo run
```

这将编译并运行项目，输出结果将会在终端中显示。

### 发布项目

要发布项目，只需在项目根目录下运行 `cargo build --release` 命令：

```
$ cargo build --release
```

这将会生成一个优化后的可执行文件，该文件在 `target/release` 目录下生成。该可执行文件可以传递给其他人使用，无需安装 Rust 或 Cargo。

Cargo 可以帮助 Rust 开发者自动管理依赖项和构建过程，使得开发和发布 Rust 项目变得更加简单。
