# Setting Up Royalties on an External Collection

#### Step 1:

Open the royalties contract in a new tab: [**https://etherscan.io/address/0xEa90CFad1b8e030B8Fd3E63D22074E0AEb8E0DCD#writeProxyContract**](https://etherscan.io/address/0xEa90CFad1b8e030B8Fd3E63D22074E0AEb8E0DCD#writeProxyContract)

#### Step 2:

Make sure the active tab is **Contract. **Next, make sure **Write as Proxy** is selected near the top, and then click **Connect to Web3**.

![](<../.gitbook/assets/image (7).png>)

#### Step 3:&#x20;

To set the royalties for the entire collection, expand the **setRoyaltiesByToken **function.\
\
You will now need to enter the **collection address** in the** Token (Address)** Field followed by the **tuple (An example of a tuple is below) **for royalties. \
****\
**The first part of the tuple must be the address where you'd like to receive the royalties, the second part is the percentage as Basis Points ie: 1000 = 10% Royalties.**

Below is an example of a tuple which gives the user (**0x6C1AaC9EAd0a2c0D328309fbb2cf940F49d26126**) **1% royalties** on items in the collection. \
\
**Please note the maximum royalties value is 10000 (100%).**

```
[["0x6C1AaC9EAd0a2c0D328309fbb2cf940F49d26126", 100]]
```

In the screenshot **below** you can see that on the **collection (0x4008c2482357632b06526b492c143f4e73ff1b0d)** the **user (0x6C1AaC9EAd0a2c0D328309fbb2cf940F49d26126)** receives** 2.5% (250) Royalties.**

![](<../.gitbook/assets/image (3) (1).png>)

Now we can go ahead and click on write which will bring up your connected wallet and ask you to pay gas fees to execute a transaction.&#x20;

![](<../.gitbook/assets/image (4).png>)

Now that Royalties have been set up, royalties will be paid out on every sale in that collection!\
\
Below is an example of a purchase transaction with annotations on what each fee is for:

![](<../.gitbook/assets/image (6) (1).png>)

You now have royalties across Rarible Protocol Platforms, Congratulations!
