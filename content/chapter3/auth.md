+++
title = "JWT Authentication"
weight = 5
+++

## authed
By adding the `authed` keyword and an `@claim` parameter, you can generate code that uses JWT authentication.

```tyml
type Token {
    token: string
}

type Claim {
    iss: string
    sub: string
    iat: int
    exp: int
}

interface API {
    /// A method to pre‑register and return a token
    function register(user_name: string) -> Token

    /// Get the user name while logged in
    authed function get_user_name(@claim: Claim) -> string
}
```

## Generated Code
When you use JWT auth, a `JwtValidator` is generated and you are required to implement token verification.

- Rust

```rs
/// Implement this for your server struct.
///
/// ## Example
/// ```
/// impl JwtValidator for YourServerStruct {
///     fn validate<T: serde::de::DeserializeOwned>(token: &str) -> Result<T, ()> {
///         let claim = jsonwebtoken::decode(
///             token,
///             &DecodingKey::from_secret("* your secret key *".as_bytes()),
///             &Validation::default(),
///         )
///         .map_err(|_| ())?
///         .claims;
///
///         Ok(claim)
///     }
/// }
/// ```
pub trait JwtValidator {
    fn validate<T: serde::de::DeserializeOwned>(token: &str) -> Result<T, ()>;
}
```

After generation, implement it to enable JWT.
(For the Rust implementation, you need the `jsonwebtoken`, `async-trait`, and `tokio(features = ["full"])` crates.)
```rs
use api::{
    serve,
    types::{Claim, JwtValidator, API, Token},
};
use async_trait::async_trait;
use jsonwebtoken::{DecodingKey, EncodingKey, Header, Validation};

struct Server {}

#[async_trait]
impl API for Server {
    async fn register(&self, user_name: String) -> String {
        let token = jsonwebtoken::encode(
            &Header::default(),
            &Claim {
                iss: "localhost".to_string(),
                iat: 0,
                sub: user_name,
                exp: i64::MAX,
            },
            &EncodingKey::from_secret(SECRET.as_bytes()),
        )
        .unwrap();

        Token { token }
    }
    async fn get_user_name(&self, claim: Claim) -> String {
        println!("Login : {}", &claim.sub);

        claim.sub
    }
}

static SECRET: &'static str = "RUST IS GOOD!";

impl JwtValidator for Server {
    fn validate<T: serde::de::DeserializeOwned>(token: &str) -> Result<T, ()> {
        let claim = jsonwebtoken::decode(
            token,
            &DecodingKey::from_secret(SECRET.as_bytes()),
            &Validation::default(),
        )
        .map_err(|_| ())?
        .claims;

        Ok(claim)
    }
}

#[tokio::main]
async fn main() {
    let server = Server {};
    serve(server, "localhost:3000").await.unwrap();
}
```

On the client side, authed methods require a token as the first argument.
```ts
class API {
    //...
    // Methods marked with "authed" receive __token: string as the first parameter
    public async get_user_name(__token: string): Promise<string> {
        //...
    }
}
```
```ts
async function main() {
    const api = new API("http://localhost:3000");

    const token = await api.register("typescript user!");

    // Call using the token returned from register
    const name = await api.get_user_name(token.token);
}
```
