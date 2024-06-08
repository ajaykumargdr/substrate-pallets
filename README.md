# Substrate Pallets Repository

## Table of Contents
- [Overview](#overview)
- [Pallets](#pallets)
  - [Custom Token Pallet](#custom-token-pallet)
  - [Guessing Number Game Pallet](#guessing-number-game-pallet)
- [Usage](#usage)
- [Contributing](#contributing)
- [License](#license)

## Overview

This repository contains two Substrate pallets implemented within a Cargo workspace. These pallets can be integrated into a Substrate-based blockchain runtime. The two pallets included are:

1. **Custom Token Pallet**: Implements a simple custom token that allows users to exchange native tokens for custom tokens and transfer these custom tokens between accounts.
2. **Guessing Number Game Pallet**: Implements a basic guessing number game where users can set a target number and others can make guesses to match the target.

## Pallets

### Custom Token Pallet

The Custom Token Pallet allows users to:

- Exchange native tokens for custom tokens.
- Transfer custom tokens between accounts.
- Query the balance of custom tokens.

#### Features
- **Token Exchange**: Users can exchange their native tokens for custom tokens at a fixed rate.
- **Token Transfer**: Users can transfer their custom tokens to other accounts.
- **Balance Query**: Users can check their custom token balance.

#### Usage
- **exchange_native_to_custom_token**: Exchanges a specified amount of native tokens for custom tokens.
- **my_transfer**: Transfers custom tokens from one account to another.
- **get_balance**: Retrieves the custom token balance of the caller.

### Guessing Number Game Pallet

The Guessing Number Game Pallet allows users to:

- Set a target number.
- Make guesses to match the target number.
- Remove the target number.

#### Features
- **Set Target**: Root users can set a target number.
- **Guess Number**: Users can make guesses to try and match the target number.
- **Remove Target**: Root users can remove the current target number.

#### Usage
- **set_target**: Sets a new target number (root only).
- **check_with**: Checks a user's guess against the target number.
- **remove_target**: Removes the current target number (root only).

## Usage

Add the pallets to your runtime's `Cargo.toml`:

```toml
[dependencies]
pallet-custom-token = { git = "https://github.com/ajaykumargdr/substrate-pallets", branch = "main", default-features = false }
pallet-guessing-game = { git = "https://github.com/ajaykumargdr/substrate-pallets", branch = "main", default-features = false }

[features]
default = ["std"]
std = [
    "pallet-custom-token/std",
    "pallet-guessing-game/std",
    # other std features...
]
```

Configure the pallets in your runtime:

```rust
impl pallet_custom_token::Config for Runtime{
	type RuntimeEvent = RuntimeEvent;
	type Currency = Balances;
}

impl pallet_guessing_number_game::Config for Runtime{
	type RuntimeEvent = RuntimeEvent;
}
```

Add the pallets to your runtime module:

```rust
#[frame_support::runtime]
mod runtime {
    use frame_support::runtime;

    ...

	#[runtime::pallet_index(8)]
	pub type CustomToken = pallet_custom_token;

	#[runtime::pallet_index(9)]
	pub type GuessGame = pallet_guessing_number_game;
}
```

## Contributing

We welcome contributions from the community! Please read our [Contributing Guide](CONTRIBUTING.md) to get started.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

Feel free to reach out for any queries or support. Happy coding! 🚀