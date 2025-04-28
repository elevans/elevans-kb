# Foreign Function Interface (FFI)

## Export Rust functions using C ABI

```rust
// some rust function
#[no_mangle]
pub extern "C" fn foo(x: i32) -> i32 {
    x
}
```

## Verify symbol export

You can verify that methods made available for FFI using the C ABI convention with the `binutils` tool
`nm`.

```bash
nm -g libimgal.so
```
