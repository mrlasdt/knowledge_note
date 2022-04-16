# Testing and BenchMarking

## Testing

Checking logs of runtime module
+ Mocking runtime Enviroment.
+ Uinit test logic for module pallet.


``` 
cargo test
cargo test -p <pallet name>
cargo test -p <pallet name> tests::<uint test name> -- -- exact
```

## Mocking

+ Mock runtime enviroment

+ Mock runtime storage

## Debugging

run Debug

```
RUST_LOG=runtime=debug ./target/release/node-template --dev
```
## Weight

weight is a representation of block execution time.

+ Weight depends on the computation capacity of each computer:
  + Including: Processor, Memory, Hard Drive, OS, Rust Compiler, DB
  + $10^12$ weight units  = 1 seconds, or 1000 weight units = 1 nano second.
+ Fee: Final Fee = base fee + weight fee + length fee + tip
  + base fee: base weight.
  + weight fee: proportion to execution time. 
  + length fee: encoded length of transaction.
  + tip: optional.
syntax: 
**Development**
``` 
#[pallet::weight(100_000)]
fn do_something(){
    // ...
}
```
**Production**
```
#[pallet::weight(T::DbWeight::get().reads_writes(1,2) + 20_000)]
fn do_something(){
    // ...
}
```

## Benchmarking
+ Stop user spam transactions.
+ developers adjust transaction fee for user.
+ *Use "Worst case" for benchmarking.*

template
```
benchmarks! {
    benchmark_name {
        /* set-up initial state */
}: {
    /* the code to be benchmarked */
} verify {
    /* verifying final state */
    }
}
```
Benchmarking steps
```
step 1: use marco benchmark! for testing worst case for pallet
step 2: enable features runtime-benchmark in Cargo.toml in runtime.
step 3: add_benchmark!
step 4: cargo build --release --features runtime-benchmarks
step 5: ./target/release/node-template benchmark
```

