# same thing but with some basic improvements 

rust/src/elf.rs — was panicking on any bad .ko (OOB indexing). Now bounds-checked parse, safe symname (<bad-*> instead of panic), rd/wr/splice return Result.

rust/src/credmod.rs — propagates those ?, validates rela sizes, build_cfg range + line-boundary checks, replaces unwrap() on sec_idx.

rust/src/json.rs — fixed UTF-8 corruption (c as char), OOB in lit/\u, empty numbers, adds depth/size caps.

rust/src/asm.rs — fixed balign dropping NOPs when misaligned, fail-fast on undefined labels.

rust/src/adb.rs + orchestrate.rs — added sh_escape(), all device_path/service names quoted, push() failures now die instead of silent, parse_ws uses last pair + overflow check, adbd_pid/mod_name/WaitShell pid validation, Stager idempotent start + early Java error break.

rust/src/main.rs/target.rs — --settle validates 0..60s finite, target path checks, path-traversal guard in local_path, dev subcommands validate argc, test-aes validates IV hex.

port.py — run() checks rc/timeout, debugfs_dump validates paths, init_array validates ELF/bounds, errors to stderr.
README.md — --settle default 3 → 0.3 to match code.

Tests added: aes.rs FIPS-197 vector, json.rs parse/reject/UTF-8, credmod.rs cfg layout, adb.rs escape/b64.
