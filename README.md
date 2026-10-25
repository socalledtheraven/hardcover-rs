# hardcover-rs

- A Rust library for the [Hardcover](https://hardcover.app/) GraphQL API. 
- Fully asynchronous with tokio and reqwest.
- Matches the API spec for the data model - it's really easy to convert from an existing query.
- Handles all the GraphQL and network side of things.
  - All you have to do is await a constructor and all the data is right there!
- Doesn't yet support POST requests, editing user libraries or nested requests
  - i.e. if you want all the books an author has written, you will have to use a for loop (it's coming!)

## Usage

### Basic Example

```rust
use hardcover_rs::{HardcoverClient, Book, BaseHardcoverItem};

#[tokio::main]
async fn main() -> Result<(), Box<dyn std::error::Error>> {
    let api_key = std::env::var("API_KEY").expect("API_KEY must be set");
    let client = HardcoverClient::new(api_key);

    let lotr = Book::from_id(377938, &client).await?;
    println!("Lord of the Rings: {:#?}", lotr);
    println!("Editions: {}", lotr.editions_count);

    Ok(())
}
```

## Documentation

Generate and view documentation locally:

```bash
cargo doc --open
```

## License

Licensed under LGPLv2.
