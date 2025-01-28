# eventing_rs

Thread-safe one-to-many event system. Simple and easy to use, no complicated setup required.

## Event Publishing

![Publishing](docs/README/structure.drawio.svg)

## Examples

The following example demonstrates how to create an event bus, subscribe players to it, and send events to the bus.

```rust
fn main() {
    // Create a bus
    let bus = EventBus::new().into_shared();

    // Create players and subscribe them to the bus
    let player1 = Player { id: 1 }.into_shared();
    let player2 = Player { id: 2 }.into_shared();
    bus.lock().unwrap().subscribe(player1);
    bus.lock().unwrap().subscribe(player2);

    // Create an input and connect it to the bus
    let input = Input::new(bus.clone());

    // Send some events
    input.send_move(1, 1.0, 2.0);
    input.send_atack(2);
}
```

For the full example, see the [examples/basic_game_events](examples/basic_game_events) directory.
