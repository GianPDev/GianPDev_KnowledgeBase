### Dioxus (web) incompatibility
- sentry
- sentry-tracing

## Using tracing with Dioxus (web)
```toml
[dependencies]
tracing = "0.1.36"
tracing-wasm = "^0.2"
wasm-bindgen = "^0.2"
console_error_panic_hook = "0.1.7"
```

```rust
//wasm_tracing.rs

use std::env;

use tracing::{debug, error, info, warn};
use tracing_subscriber::prelude::*;
use wasm_bindgen::prelude::*;

#[wasm_bindgen]
pub fn init_tracing() {
    console_error_panic_hook::set_once();
    tracing_wasm::set_as_global_default();

    debug!("debug! wasm_tracing.rs check");
    info!("info! wasm_tracing.rs check");
    warn!("warn! wasm_tracing.rs check");
    error!("error! wasm_tracing.rs check");
}
```

```rust
use crate::wasm_tracing;
use dioxus::prelude::*;
use tracing::{debug, error, info, warn};
use wasm_bindgen::prelude::*;

#[wasm_bindgen]
pub fn run() {
    wasm_tracing::init_tracing();
    info!("app.rs info!");
    warn!("app.rs warn!");
    error!("app.rs error!");
    dioxus::web::launch(hello_world);
}

fn hello_world(cx: Scope) -> Element {
    info!("Hello wasm info!");
    cx.render(rsx! {
        div {
            "Hello, wasm!"
        }
    })
}
```