We've created a fork of Zecwallet-Lite, originally from the repository at https://github.com/adityapk00/zecwallet-lite. The need for this fork arose because the original developer did not address an issue where the wallet's transaction fee was set at 1000 zat. This became problematic especially during a spam attack on the ZCash network when transactions with such fees were no longer being included in miner blocks.

Our fondness for Zecwallet-Lite drove us to address this issue ourselves. With this update, we've made a singular change: the transaction fee has been revised from 1000 zat to 10000 zat. Every other aspect of the wallet's functions and logic remains unchanged.

You can choose whichever version you feel best suits your needs.


## Note: Even though this version retains all the logic from the original repository, always adhere to the "zero trust" principle and use this release at your own risk. We are *not* responsible for any malfunctions and potential damage. However, we guarantee on our part that this version preserves 100% of the original code, except for the adjustment of the fee from 1000 to 10000 zat.

Note: You have the flexibility to adjust the transaction fee as per your needs. To do this:

 Clone the following three repositories into a single directory: [zecwallet-lite](https://github.com/kattywood/zecwallet-lite), [zecwallet-light-cli](https://github.com/kattywood/zecwallet-light-cli), and [librustzcash](https://github.com/kattywood/librustzcash). Or  download them all at once from [here ](https://github.com/kattywood/zecwallet-lite/releases/download/v1.8.8_bump_fee/Source.code.MAIN.zip)

Navigate to librustzcash\zcash_primitives\src\transaction\components\amount.rs and on line 10, modify the value from "10000" to your preferred amount in the line
* pub const DEFAULT_FEE: Amount = Amount(10000).
 
Once the changes are made, you can then compile the project using the source code as per the instructions given below.
	
## ZecWallet Lite
Zecwallet-Lite is z-Addr first, Sapling compatible lightwallet client for Zcash. It has full support for all Zcash features:
- Send + Receive fully shielded transactions
- Supports transparent addresses and transactions
- Full support for incoming and outgoing memos
- Fully encrypt your private keys, using viewkeys to sync the blockchain

## Download
Download compiled binaries from our [release page](https://github.com/kattywood/zecwallet-lite/releases/tag/v1.8.8_bump_fee)

## Privacy
* While all the keys and transaction detection happens on the client, the server can learn what blocks contain your shielded transactions.
* The server also learns other metadata about you like your ip address etc...
* Also remember that t-addresses don't provide any privacy protection.


### Note Management
Zecwallet-Lite does automatic note and utxo management, which means it doesn't allow you to manually select which address to send outgoing transactions from. It follows these principles:
* Defaults to sending shielded transactions, even if you're sending to a transparent address
* Sapling funds need at least 5 confirmations before they can be spent
* Can select funds from multiple shielded addresses in the same transaction
* Will automatically shield your transparent funds at the first opportunity
    * When sending an outgoing transaction to a shielded address, Zecwallet-Lite can decide to use the transaction to additionally shield your transparent funds (i.e., send your transparent funds to your own shielded address in the same transaction)

## Compiling from source
Zecwallet Lite is written in Electron/Javascript and can be build from source. It will also automatically compile the Rust SDK needed to run Zecwallet Lite.

#### Pre-Requisites
You need to have the following software installed before you can build Zecwallet Lite from source code:

* [Nodejs v18.16.1 or higher](https://nodejs.org)
* [Yarn](https://yarnpkg.com)
* [Rust v1.65+](https://www.rust-lang.org/tools/install)


```
git clone https://github.com/kattywood/zecwallet-lite
git clone https://github.com/kattywood/librustzcash
git clone https://github.com/kattywood/zecwallet-light-cli
cd zecwallet-lite

yarn install
yarn build
```
In case of "ERR_OSSL" compilation errors, use the command:
* for Linux:
```
export NODE_OPTIONS=--openssl-legacy-provider
```

* for Windows:
```
set NODE_OPTIONS=--openssl-legacy-provider
```
or
```
$env:NODE_OPTIONS = "--openssl-legacy-provider"
```

* To start in locally, run
```
yarn start
```

* To compile for specific platforms:
For Windows:
```
yarn dist:win
```
For Linux:
```
yarn dist:linux
```

For macOS:
```
yarn dist:mac
```

_PS: Zecwallet-Lite is NOT an official wallet, and is not affiliated with the Electric Coin Company in any way._
