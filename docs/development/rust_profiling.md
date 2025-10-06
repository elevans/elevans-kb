# Rust application profiling

## Using `cargo flamegraph`

If you don't have it, install `flamegraph` with `cargo install flamegraph`. Next add these to your release profile in the `Cargo.toml`.

```
[profile.release]
debug = true
strip = false
```

Before generating the flamegraph, set the perf paranoid level:

```bash
sudo sysctl -w kernel.perf_event_paranoid=-1
echo 0 | sudo tee /proc/sys/kernel/kptr_restrict
cargo flamegraph
```
