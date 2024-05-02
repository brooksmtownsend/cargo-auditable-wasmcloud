# cargo auditable wasmcloud http-hello-world

## Prerequisites
Install `cargo-auditable` from the Wasm branch, and cargo-audit

```bash
cargo install cargo-audit
cargo install cargo-auditable --git https://github.com/rust-secure-code/cargo-auditable --branch wasm
```

## Setup
Modify wasmcloud.toml to use `cargo auditable`:
```toml
name = "http-hello-world"
version = "0.1.0"
language = "rust"
type = "component"

[component]
wit_world = "hello"
wasm_target = "wasm32-wasi-preview2"

build_command = "cargo auditable build --target wasm32-wasi"
build_artifact = "target/wasm32-wasi/debug/http_hello_world.wasm"
```

## Build
Run `wash build`, or just run the above build command manually:

```bash
cargo auditable build --target wasm32-wasi
```

## Inspect

You can manually verify that the information was embedded in the component using [wasm-custom-section](https://github.com/xtuc/wasm-custom-section)

```bash
➜ wasm-custom-section ./target/wasm32-wasi/debug/http_hello_world.wasm show .dep-v0
Section `.dep-v0` (535 bytes):
Length: 535 (0x217) bytes
0000:   78 9c a5 55  ed 8e db 20  10 7c 17 ff  c6 16 60 c7   x..U... .|....`.
0010:   f9 78 95 2a  aa 08 6c 13  7a 18 7c 80  f3 a1 d3 bd   .x.*..l.z.|.....
0020:   7b 49 da b4  31 24 35 b9  fc b3 90 67  66 77 76 16   {I..1$5....gfwv.
0030:   3e 8a 9e f1  37 b6 05 57  ac be 7d 14  9a 75 50 ac   >...7..W..}..uP.
0040:   0a a6 4f 3b  73 28 50 b1  07 eb a4 d1  e1 88 54 b8   ..O;s(P.......T.
0050:   5a d0 70 e4  cc 60 f9 f9  27 6e 99 07  57 49 53 7c   Z.p..`..'n..WIS|
0060:   a2 bf c8 8d  f4 3f 14 db  ba 11 96 56  b3 0a 4f 42   .....?.....V..OB
0070:   e1 7d 90 7b  a6 40 fb 44  98 4c 82 77  cc ed 36 d6   .}.{.@.D.L.w..6.
0080:   1c f4 08 1b  90 4d 35 9b  06 03 7f 8b  70 cd 23 4d   .....M5.....p.#M
0090:   54 08 e8 41  0b d0 5c 5e  4c a3 74 7d  4b e5 7d 5f   T..A..\^L.t}K.}_
00a0:   ee 40 29 53  1e 8c 55 22  2e 67 ec 83  32 9c a9 3b   .@)S..U".g..2..;
00b0:   94 f3 35 2a  ac 31 be 58  79 3b c0 0d  bd 14 25 b3   ..5*.1.Xy;....%.
00c0:   a0 59 64 2f  cd 70 48 06  81 63 c7 fa  04 da e6 36   .Yd/.pH..c.....6
00d0:   8a 6a 44 66  b7 cd 4a 6f  58 3a ab e9  52 14 6c 08   .jDf..JoX:..R.l.
00e0:   5d 44 d6 d0  8c 41 29 b3  4d e6 44 a7  f5 7a 6b 78   ]D...A).M.D..zkx
00f0:   d9 31 6e 0d  4d 33 9d 3d  67 72 db fa  fb 60 3c 24   .1n.M3.=gr...`<$
0100:   64 75 ae 97  64 44 66 4f  43 6a e3 7c  b2 2d 07 5d   du..dDfOCj.|.-.]
0110:   c0 24 48 4a  33 90 56 a4  d5 53 8c f3  90 df 05 58   .$HJ3.V..S.....X
0120:   b9 7f 82 e0  4e ff 88 50  44 f1 3a a1  fe e9 8c be   ....N..PD.:.....
0130:   93 a9 5c 63  17 88 c4 29  75 1d 53 6a  0f 3c 62 25   ..\c...)u.Sj.<b%
0140:   75 95 61 54  2f 8e f1 0a  87 d0 e5 76  b9 18 d5 71   u.aT/......v...q
0150:   d2 d1 ee e1  aa 7d d2 b0  51 6c 06 2d  b9 11 50 4a   .....}..Ql.-..PJ
0160:   71 f7 ce 9c  ee ee 4a e0  60 db 05 0a  e6 65 e2 3d   q.....J.`....e.=
0170:   21 19 37 f7  95 e7 28 45  b2 d4 cd 24  fa c0 5c 57   !.7...(E...$..\W
0180:   86 46 03 83  8d e1 98 56  b9 0e 2d d7  31 67 07 9e   .F.....V..-.1g..
0190:   09 e6 d9 0b  a4 18 cd 43  9a 10 69 11  09 1f 4b 44   .......C..i...KD
01a0:   1b 44 db 58  a8 67 d6 bd  54 3a 39 ab  34 23 5a e9   .D.X.g..T:9.4#Z.
01b0:   cb 4d b8 b1  b7 10 3f 68  b4 c9 a6 a5  4b 54 93 07   .M....?h....KT..
01c0:   ac 25 37 16  be 4e 8d 51  5d 3f 62 b6  fe eb bc 0f   .%7..N.Q]?b.....
01d0:   cb b5 83 f3  af 94 db 04  8b e9 0c d1  05 aa e9 ff   ................
01e0:   34 7e 3f 13  af 28 5d af  b6 8b 16 8e  b5 b8 e9 7a   4~?..(]........z
01f0:   a3 e3 7d 7d  36 94 97 c0  e0 7f c9 3c  c7 32 34 d7   ..}}6......<.24.
0200:   de 99 ca cb  e1 c4 a8 fd  a3 d6 dc 08  d6 97 3d 58   ..............=X
0210:   7f fe 02 bb  00 37 1a                                .....7.
```

Inspect the binary with `cargo audit` (this step currently fails):
```bash
cargo audit bin ./target/wasm32-wasi/debug/http_hello_world.wasm
```

Error message:
```console
➜ cargo audit bin ./target/wasm32-wasi/debug/http_hello_world.wasm
    Fetching advisory database from `https://github.com/RustSec/advisory-db.git`
      Loaded 623 security advisories (from /Users/brooks/.cargo/advisory-db)
    Updating crates.io index
error: parse error: could not extract dependencies from binary ./target/wasm32-wasi/debug/http_hello_world.wasm
Caused by:
  -> Failed to parse the binary: Not an executable file
  -> Not an executable file
```
