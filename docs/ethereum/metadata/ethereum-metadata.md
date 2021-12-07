# Ethereum Metadata

Providing Assets Metadata allows applications to extract data for digital assets and display them in the application.

URIs usually represent digital assets in a smart contract. Metadata allows assets to have additional properties, such as name, description, and image.

## tokenURI

To get metadata for ERC-721 and ERC-1155, you need to return the URI. To do this, use the function:

* `tokenURI` in [ERC-721](https://github.com/rarible/protocol-contracts/blob/master/tokens/contracts/erc-721/ERC721Upgradeable.sol)
* `uri` in [ERC-1155](https://github.com/rarible/protocol-contracts/blob/master/tokens/contracts/erc-1155/ERC1155Upgradeable.sol).

ERC-721

```
    /**
     * @dev See {IERC721Metadata-tokenURI}.
     */
    function tokenURI(uint256 tokenId) public view virtual override returns (string memory) {
        require(_exists(tokenId), "ERC721Metadata: URI query for nonexistent token");

        string memory _tokenURI = _tokenURIs[tokenId];
        string memory base = baseURI();

        // If there is no base URI, return the token URI.
        if (bytes(base).length == 0) {
            return _tokenURI;
        }
        // If both are set, concatenate the baseURI and tokenURI (via abi.encodePacked).
        if (bytes(_tokenURI).length > 0) {
            return LibURI.checkPrefix(base, _tokenURI);
        }
        // If there is a baseURI but no tokenURI, concatenate the tokenID to the baseURI.
        return string(abi.encodePacked(base, tokenId.toString()));
    }
```

ERC-1155

```
    /**
     * @dev See {IERC1155MetadataURI-uri}.
     *
     * This implementation returns the same URI for *all* token types. It relies
     * on the token type ID substitution mechanism
     * https://eips.ethereum.org/EIPS/eip-1155#metadata[defined in the EIP].
     *
     * Clients calling this function must replace the `\{id\}` substring with the
     * actual token type ID.
     */
    function uri(uint256) external view virtual override returns (string memory) {
        return _uri;
    }
```

The `tokenURI` or `uri` function returns an HTTP or IPFS URL. When requesting the URL, should be returned JSON with metadata for the token.

## Metadata Structure

The Rarible Ethereum Protocol supports the Metadata structure according to the standards [EIP-721](https://eips.ethereum.org/EIPS/eip-721) and [EIP-1155](https://eips.ethereum.org/EIPS/eip-1155).

Example of a Metadata structure for ERC-1155 NFT:

```json
{
    "name": "CryptoParrot#17",
    "description": "The CryptoParrot is a collection of 10,000 unique Parrot NFTs",
    "attributes": [
        {
            "key": "/background",
            "value": "rust"
        },
        {
            "key": "/body",
            "value": "lavender down"
        },
        {
            "key": "/color",
            "value": "gray"
        },
        {
            "key": "/eye",
            "value": "small 1"
        },
        {
            "key": "/head",
            "value": "navy blue nightcap"
        },
        {
            "key": "/mouth",
            "value": "yellow 6"
        }
    ],
    "image": {
        "url": {
            "ORIGINAL": "ipfs://ipfs/QmUoc2LDDnHxHsesLXtpxTLupzVuyfVkJomWWHmvKNCjrL/image.png"
        },
        "meta": {
            "ORIGINAL": {
                "type": "image/png",
                "width": 999,
                "height": 999
            }
        }
    }
}
```

Description of properties:

| name |  | Name of the item |
| --- | --- | --- |
| description |  | A human-readable description of the item |
| attributes | key, value | These are the attributes for the item |
| image | url | This is the URL to the image of the item |
|  | meta | This is meta-information about media. Include type, width, and height |
| animation | url | This is the URL to the animation of the item |
|  | meta | This is meta-information about media. Include type, width, and height |

For the Rarible Ethereum Protocol, it does not matter where the Metadata for NFT will be placed. [See the example](ipfs-example.md) of uploading and using metadata with [IPFS](https://ipfs.io/).
