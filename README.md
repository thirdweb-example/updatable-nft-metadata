# Updatable NFT Metadata

Create a NFT drop with updatable metadata.

## Setup

To run the project, first clone this repository, and then run one of the following commands to install the dependencies:

```bash
npm install
# or
yarn install
```

Next, you need to create a .env.local file and add the PRIVATE_KEY variable to it with the private key of the wallet you have used to create the NFT drop:

```
PRIVATE_KEY=...
```

Now, update the `db.json` file with the NFT drop's data. Once done, push your code to a repository.

Finally, go to [`scripts/upload-nfts.mjs`](scripts/upload-nfts.mjs) and update your drop address and metadata files. The metadata file urls should be in this format: `https://my-json-server.typicode.com/<your_username>/<your_repo_name>/nfts/<id>.`

## How It Works

Using the `.fromPrivateKey` method from `ThirdwebSDK` we initialise the sdk:

```mjs
import { ThirdwebSDK } from "@thirdweb-dev/sdk";
import { config } from "dotenv";

config();

const sdk = ThirdwebSDK.fromPrivateKey(process.env.PRIVATE_KEY, "mumbai");
```

We then use the `.getContract` method to get the NFT drop:

```mjs
const drop = await sdk.getContract("DROP_ADDRESS", "nft-drop");
```

Finally, we batch upload the NFTs using the centralized metadata files:

```js
try {
  await drop.createBatch([
    "https://my-json-server.typicode.com/thirdweb-dev/updatable-nft-metadata/nfts/0",
    "https://my-json-server.typicode.com/thirdweb-dev/updatable-nft-metadata/nfts/1",
  ]);
  console.log("uploaded all nfts");
} catch (error) {
  console.log(error);
}
```

## Join our Discord!

For any questions, suggestions, join our discord at [https://discord.gg/thirdweb](https://discord.gg/thirdweb).
