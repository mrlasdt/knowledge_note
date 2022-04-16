# Implement log for struct. 
## Struct without Generic type <T>

``` rust
#[derive(Clone, Encode, Decode, PartialEq, RuntimeDebug, TypeInfo, MaxEncodedLen)]
struct Metadata {
    name: Vec<u8>,
    age: u8,
}

let metadata = Metadata{
    name: b"DVD".to_vec(),
    age: 25u8,
}
log::info!("{:?}", metadata);
```
*RuntimeDebug*: already implement display function for normal struct.
## Struct with Generic type
Need to implement display function for generic type struct. 
```rust
#[derive(Clone, Encode, Decode, PartialEq, TypeInfo, MaxEncodedLen)]
pub struct Kitty<T: Config>{
    pub dna: [u8;16],
    pub price: Option<BalanceOf<T>>, 
    pub gender: Gender,
    pub owner: <T as frame_system::Config>::AccountId,
}
impl<T:Config> sp_std::fmt::Display for Kitty<T> {
    fn fmt(&self, f: &mut fmt::Formatter<'_>) -> sp_std::fmt::Result {
        write!(f, "dna: {:?}, price: {:?}, gender: {:?}, owner: {:?}", self.dna, self.price, self.gender, self.owner)
    }
}
log::info("kitty: {:?}", kitty);
```
**Debug Command** RUST_LOG=runtime=debug ./target/release/node-template --dev

## Test
``` rust
#[cfg(test)]
mod mock];

#[cfg(test)]
mod tests;
```