# Contract Wallets

Example implementation: [https://rinkeby.etherscan.io/address/0x998Cf6fDd7FF1EB258c288762284142D28D0ee39\#code](https://rinkeby.etherscan.io/address/0x998Cf6fDd7FF1EB258c288762284142D28D0ee39#code)

EIP1271 allows a contract to delegate authorized signers. Usually EIP1271 expects an authorized delegate to submit a signature via the contract, and uses typical ECrecover to see if the signature is valid.

EIP1271 returns `valid signature: true**` if the signature is valid & the signer is authorized by the contract

\*\* not actually `true`, but instead a magic value to guard against mistaken 'true' bit

The Rarible contract checks if the signature is valid with the following code

```text
    require(
        ERC1271(order.maker).isValidSignature(_hashTypedDataV4(hash), signature) == MAGICVALUE,
        "contract order signature verification error"
    );
```

