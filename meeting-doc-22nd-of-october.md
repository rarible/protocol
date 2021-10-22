Meeting document for dev meeting on the 22nd of October.

### Github

None. There are two "unanswered" questions that on which we're waiting on a reply from the question owner. 

### Discord 

Some matters have been raised in the #dev-general channel to be discussed in today's meeting. Apart from discussing those, we will also be discussing the questions that weren't properly answered throught the past 7 days, and we'll follow up individually with everyone who's listed down below for a question. 

All people listed below have also been invited to participate this dev call.

```owenmurovec#8687```

Quote: "Trying to use the encodeOrder endpoint but getting an error response (Using the exact example request from the docs https://docs.rarible.org/exchange/creating-a-sell-order):
{
"code": "BAD_REQUEST",
    "message": "Instantiation of [simple type, class com.rarible.protocol.dto.RaribleV2OrderFormDto] value failed for JSON property signature due to missing (therefore NULL) value for creator parameter signature which is a non-nullable type\n at [Source: (io.netty.buffer.ByteBufInputStream); line: 24, column: 1] (through reference chain: com.rarible.protocol.dto.RaribleV2OrderFormDto[\"signature\"])",
    "status": 400
}

According to the API reference (https://api-reference.rarible.com/#operation/encodeOrder), the signature field should be optional but seems like that's what's causing the error? Tried adding the signature field as an empty string "" or as "0x" and it seems to work however it gives an EIP712 type signMessage when I need an EIP1271 type.

Anyone know what could be going wrong? or if there's a specific value I can set signature to for an EIP1271 type instead?"


```richexplorer.eth#8225```

Quote: "Hi, I am trying to lazy mint NFT using this asset creation article https://docs.rarible.org/asset/creating-an-asset 

But I am getting below 400 with invalid token, its missing creator address. I checked a lot of times and not sure what needs to be done

 data: {
    }
      code: 'VALIDATION',
      message: 'TokenId Token(id=0x6ede7f3c26975aad32a475e1021d8f6f39c89d82, owner=null, name=Rarible, symbol=RARI, status=CONFIRMED, features=[MINT_AND_TRANSFER, APPROVE_FOR_ALL], standard=ERC721, version=1) must start with first creator address',
      status: 400


Did anyone face this? Can anyone help me out in this or if there is a way to see more logs?"


```fruitybits#4442```

Quote: "another royalties question 🙂 I'm implementing some ERC721 contracts on Polygon. I want them to be ready to use Rarible Royalties when Rarible supports Polygon/Matic. Is there anything I can implement now (e.g. Royalties V1 from the docs) or do I need to sit tight?"
