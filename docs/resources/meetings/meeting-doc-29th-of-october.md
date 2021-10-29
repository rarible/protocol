Meeting document for dev meeting on the 29th of October.

Github discussions: 

https://github.com/rarible/protocol/discussions/142 ```whitespace#2877```

https://github.com/rarible/protocol/discussions/11 - related to spam NFT's being minted to someone's collection

Github issues: 

Most important: https://github.com/rarible/protocol/issues/148 ```owenmurovec#8687```

https://github.com/rarible/protocol/issues/147 ```Jaacob#1962``` and ```Branko#7207```

https://github.com/rarible/protocol/issues/143 ```tgb29#1533```

https://github.com/rarible/protocol-ethereum-sdk/issues/52 from ```inartin#9707```



Discord:

```chusla#6031```

Quote: "could we get an update on latest browser compatible sdk as well that would be much appreciated if there is any way at all to include that in next week's release for tezos etc that would unblock us thanks!"

Answer: 

```mynamebrody#5466```

Quote: "I think I'm having issues with the encodeOrder endpoint as it wants a signature but that's not required for this call yet so I haven't been including it. But adding the field with an empty value gets past this error, however, I don't think it should be there"

Answer:

```platocrat#4224```

Quote: "@Matt a friend just sent me this, which comes from your documentation.
![image](https://user-images.githubusercontent.com/39627934/139473674-927e2761-4805-4896-8691-90ad4fb04dcf.png)
Is this correct?
We should just fork Rarible Protocol, deploy the protocol to Polygon, then use those contracts to deploy our ERC1155 contracts?"
Just to clarify, i wish to use Rarible's contracts, which i assume to be on, Polygon to deploy our contracts 🙂 

Answer: 

```idan.angel#8635```

Quote: "Hi All, I'm looking for a Rarible API that would return the assetType for any NFT listed on the marketplace. In other words, I'm looking for something like: 
GET <API URL>?itemId=<contract address>:<token ID>

and I expect to get an answer that would contain a field with ERC721 or ERC1155 or Lazy_mint, something of that sort, so that I can use that value to create a new buy order. I haven't found anything of that sort. For some NFTs there are open orders which hold the assetType, but I'm looking for a standard way that would work on every NFT on Rarible, not just NFTs with open or past orders.

Any help would be appreciated."

Answer: 

```owenmurovec#8687```

Quote: "Trying to use the encodeOrder endpoint but getting an error response (Using the exact example request from the docs https://docs.rarible.org/exchange/creating-a-sell-order):
{
"code": "BAD_REQUEST",
    "message": "Instantiation of [simple type, class com.rarible.protocol.dto.RaribleV2OrderFormDto] value failed for JSON property signature due to missing (therefore NULL) value for creator parameter signature which is a non-nullable type\n at [Source: (io.netty.buffer.ByteBufInputStream); line: 24, column: 1] (through reference chain: com.rarible.protocol.dto.RaribleV2OrderFormDto[\"signature\"])",
    "status": 400
}

According to the API reference (https://api-reference.rarible.com/#operation/encodeOrder), the signature field should be optional but seems like that's what's causing the error? Tried adding the signature field as an empty string "" or as "0x" and it seems to work however it gives an EIP712 type signMessage when I need an EIP1271 type.

Anyone know what could be going wrong? or if there's a specific value I can set signature to for an EIP1271 type instead?"

Answer:


```richexplorer.eth#8225```

Quote: "Hi, I am trying to lazy mint NFT using this asset creation article https://docs.rarible.org/asset/creating-an-asset 

But I am getting below 400 with invalid token, its missing creator address. I checked a lot of times and not sure what needs to be done

 data: {
    }
      code: 'VALIDATION',
      message: 'TokenId Token(id=0x6ede7f3c26975aad32a475e1021d8f6f39c89d82, owner=null, name=Rarible, symbol=RARI, status=CONFIRMED, features=[MINT_AND_TRANSFER, APPROVE_FOR_ALL], standard=ERC721, version=1) must start with first creator address',
      status: 400


Did anyone face this? Can anyone help me out in this or if there is a way to see more logs?"

Answer:


```fruitybits#4442```

Quote: "another royalties question 🙂 I'm implementing some ERC721 contracts on Polygon. I want them to be ready to use Rarible Royalties when Rarible supports Polygon/Matic. Is there anything I can implement now (e.g. Royalties V1 from the docs) or do I need to sit tight?"

Answer:
