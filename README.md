# LibWally

A wrapper for [libwally-swift](https://github.com/Sjors/libwally-swift) so the Framework is avalible through the Swift Package Manager.

## Requirements

- iOS 11 or higher

LibWally is currently only avalible for iOS.

## Documentation

### Create new Bitcoin Wallet / Private Key / Mnemonic

```swift
var bytes = [Int]()
for _ in 1...32 {
    bytes.append(Int.random(in: Int.min...Int.max))
}
let entropy = BIP39Entropy(Data(bytes: bytes, count: 32))
let mnemonic = BIP39Mnemonic(entropy)!
let words = mnemonic.words
```

### Import Bitcoin Wallet

```swift
let words = ["bulk", "oven", "left", "scan", "tube", "always", "present", "abuse", "myself", "income", "hair", "husband", "ritual", "cube", "below", "luggage", "avoid", "slot", "slush", "cover", "february", "major", "give", "nothing"]
let mnemonic = BIP39Mnemonic(words)!
```

### Generate Bitcoin Address

```swift
let hdKey = HDKey(mnemonic.seedHex(), .mainnet)!
let derivationPath = "m/84'/0'/0'/0/0"
let account = try! hdKey.derive(path)
let address = account.address(.payToWitnessPubKeyHash).description
```
