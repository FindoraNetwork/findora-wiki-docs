# Prism++ SDK

The [Prism++ SDK ](https://github.com/FindoraNetwork/prismxx-sdk-tutorials)is a development kit for integrating Prism++ to DApps/Apps and utilize the privacy features from the Findora Native chain. Here are some basic exaple for using the Prism++ SDK. A complete details of the usage can be found [here](https://github.com/FindoraNetwork/prismxx-sdk-tutorials/blob/main/src/index.ts).

1. SDK Initialization&#x20;

```typescript
import * as dotenv from 'dotenv';
import { initSdk } from './utils/sdkInit';

dotenv.config();
async function main() {
  console.log('Init SDK...');
  await initSdk();
}

```

2. Send asset from Native chain to EVM chain

```typescript
import * as dotenv from 'dotenv';
import { initSdk } from './utils/sdkInit';
import { getNativeWallet, getEvmWallet } from './utils/getWallet';
import { nativeToEvm } from './prism';
import { NETWORK_CONFIG } from './config';

dotenv.config();

async function main() {
  console.log('Init SDK...');
  await initSdk();

  const findoraSdk = await import('@findora-network/findora-sdk.js');
  const { Asset: AssetApi } = findoraSdk.Api;

  console.log('Get Wallet...');
  const nativeWallet = await getNativeWallet();
  const evmWallet = await getEvmWallet();
  console.log('Run - Native To Evm');
  
  // Send FRA
  console.log('1、[send FRA]');
  await nativeToEvm(nativeWallet, evmWallet, await AssetApi.getFraAssetCode());
  // Send FRC20
  console.log('2、[send FRC20]');
  const frc20AssetCode = await findoraSdk.Api.Evm.hashAddressTofraAddress(
    NETWORK_CONFIG.tokens.FRC20,
    );
  await nativeToEvm(nativeWallet, evmWallet, frc20AssetCode);
  // Send FRC721
  console.log('3、[send FRC721]');
  const frc721AssetCode = await findoraSdk.Api.Evm.hashAddressTofraAddressByNFT(
    NETWORK_CONFIG.tokens.FRC721, //  NFT contract address on EVM
    '1', // nft tokenID on EVM
    );
  await nativeToEvm(nativeWallet, evmWallet, frc721AssetCode);
  // Send FRC1155
  console.log('4、[send FRC1155]');
  const frc1155AssetCode =
      await findoraSdk.Api.Evm.hashAddressTofraAddressByNFT(
          NETWORK_CONFIG.tokens.FRC1155, // NFT contract address on EVM
          '0', // nft tokenID on EVM
        );
  await nativeToEvm(nativeWallet, evmWallet, frc1155AssetCode);
  
  console.log('End!');
}

main().catch((err) => console.log(err.message));
```

3. Send asset from EVM chain to UTXO chain

{% code overflow="wrap" %}
```typescript
import * as dotenv from 'dotenv';
import { initSdk } from './utils/sdkInit';
import { getNativeWallet, getEvmWallet } from './utils/getWallet';
import {
  evmToNativeOfToken,
  evmToNativeOfFRC721,
  evmToNativeOfFRC1155,
} from './prism';
import { NETWORK_CONFIG } from './config';

dotenv.config();

async function main() {
  console.log('Init SDK...');
  await initSdk();

  const findoraSdk = await import('@findora-network/findora-sdk.js');
  const { Asset: AssetApi } = findoraSdk.Api;

  console.log('Get Wallet...');
  const nativeWallet = await getNativeWallet();
  const evmWallet = await getEvmWallet();
  
  console.log('Run - Evm To Native');
  
  // Send FRA
  console.log('1、[send FRA]');
  await evmToNativeOfToken(
      nativeWallet,
      evmWallet,
      '0x0000000000000000000000000000000000001000',
      'FRA',
  );
  // Sned FRC20
  console.log('2、[send FRC20]');
  await evmToNativeOfToken(
      nativeWallet,
      evmWallet,
      NETWORK_CONFIG.tokens.FRC20,
      'FRC20',
  );
  //Send FRC721
  console.log('3、[send FRC721]');
  await evmToNativeOfFRC721(
      nativeWallet,
      evmWallet,
      NETWORK_CONFIG.tokens.FRC721,
      '0', // tokenID
  );
  // Send FRC1155
  console.log('4、[send FRC1155]');
  await evmToNativeOfFRC1155(
      nativeWallet,
      evmWallet,
      NETWORK_CONFIG.tokens.FRC1155,
      '0', // tokenID
      '1', // token amount ,  amount of nft 1155 to be transffered
  );
  
  console.log('End!');
}

main().catch((err) => console.log(err.message));
```
{% endcode %}
