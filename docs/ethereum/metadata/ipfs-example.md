# Example of uploading & using Metadata with IPFS

## Uploading images to IPFS

To upload images to IPFS, will use the [Pinata](https://www.pinata.cloud) service.

Here you can see an example using Node JS to upload an image using the Pinata API.

```
const axios = require("axios");
const fs = require("fs");
const FormData = require("form-data");

export const pinFileToIPFS = (pinataApiKey, pinataSecretApiKey) => {
  const url = `https://api.pinata.cloud/pinning/pinJSONToIPFS`;
  let data = new FormData();

  data.append("file", fs.createReadStream("./yourfile.png"));

  return axios.post(url, data, {
      headers: {
        "Content-Type": `multipart/form-data; boundary= ${data._boundary}`,
        pinata_api_key: pinataApiKey,
        pinata_secret_api_key: pinataSecretApiKey,
      },
    })
    .then(function (response) {
      console.log(repsonse.IpfsHash);
    })
    .catch(function (error) {
      console.log(error)
    });
};
```

Response to the request:

```
{
    IpfsHash: // This is the IPFS multi-hash provided back for your content,
    PinSize: // This is how large (in bytes) the content you just pinned is,
    Timestamp: // This is the timestamp for your content pinning (represented in ISO 8601 format)
}
```

## Creating a Metadata file for NFT

With the `IpfsHash`, we can create a Metadata file. It will be connected to the NFT inside the blockchain network.

```
{
   "name": /* NFT Name - This must be a string */,
   "description": /* Description of the NFT - This must be a string */,
   "image": /*  IPFS Hash to our content, this must be prefixed with "ipfs://ipfs/{{ IPFS_HASH ))" - This must be a string */,
   "external_url": /* This is the link to Rarible which we currently don't have, we can fill this in shortly */,
   "animation_url": /* IPFS Hash just as image field, but it allows every type of multimedia files. Like mp3, mp4 etc */,
   // the below section is not needed.
   "attributes": [
      {
         "key": /* Key name - This must be a string */,
         "trait_type": /* Trait name - This must be a string */,
         "value": /* Key Value - This must be a string */
      }
   ]
}
```

## Adding generated Metadata to IPFS

1. Specify `external_url` in the format `${contractAddress}:${tokenId}`, for example:

```
"external_url": "https://app.rarible.com/0x60f80121c31a0d46b5279700f9df786054aa5ee5:123913"
```

2. Publish Metadata to IPFS:

```
var axios = require('axios');
var data = JSON.stringify({"name":"Test NFT","description":"Test NFT","image":"ipfs://ipfs/QmW4P1Mgoka8NRCsFAaJt5AaR6XKF6Az97uCiVtGmg1FuG/image.png","external_url":"https://app.rarible.com/0x60f80121c31a0d46b5279700f9df786054aa5ee5:123913","attributes":[{"key":"Test","trait_type":"Test","value":"Test"}]});

var config = {
  method: 'post',
  url: 'https://api.pinata.cloud/pinning/pinFileToIPFS',
  headers: { 
    'pinata_api_key': // KEY_HERE, 
    'pinata_secret_api_key': // SECRET_KEY_HERE, 
    'Content-Type': 'application/json'
  },
  data: data
};

axios(config).then(function (response) {
  console.log(JSON.stringify(response.data));
}).catch(function (error) {
  console.log(error);
});
```

Response example:

```
{
    "IpfsHash": "QmNybufJtuvWCZ355HGejvKfUXK8VeLcPA5G7CxT9MXJJp",
    "PinSize": 290,
    "Timestamp": "2021-02-10T14:06:09.255Z"
}
```

3. Attach the new `IpfsHash` to your NFT.
