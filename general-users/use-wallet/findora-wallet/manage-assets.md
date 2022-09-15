# Manage Assets



### Define New Asset[​](https://wiki.findora.org/docs/evm\_guides/use\_wallet/findora\_wallet/manage#define-new-asset) <a href="#define-new-asset" id="define-new-asset"></a>

* Creating a new asset requires you to first _**define**_ the asset. Then, to complete the process of creating a new asset you must _**issue**_ the asset (by specifying the number of units of that asset to issue). Please note, after you define the asset the number of units for that asset remains 0 and will remain 0 until you issue the asset.

![wallet21.png](https://wiki.findora.org/assets/images/wallet21-8194b4a6731650041ec220905210e023.png)

Below are the two steps needed to create a new asset:

1. Goto `Manage Assets` ⇒ `Define New Asset`
   * Fill out the input fields on the `Define New Asset` page

![wallet22.png](https://wiki.findora.org/assets/images/wallet22-e2af1ca6f53f5b541dab1cad91ed9bbd.png)

* `Asset Creator` - select the wallet address which will create the new asset
* `Asset Nickname` - enter a nickname for the asset (it can be edited later)
* `Asset Code` - this value is generated automatically by the system. You can consider this as your custom asset's unique token "ticker".
* `Asset Memo` - enter a description for your custom asset
* `Asset Decimals` - set the number of decimal places for your custom asset (up to 16 places)
* `Set a maximum # of assets to issue` - you can cap the number of units of the custom asset to a maximum value. For example, Bitcoin is capped at 21 million units by design. Please note, if you specify a maximum number of assets to issue, the number of tokens you issue during the issuance phase will be shown on the public block explorer. If you do not place a cap on the maximum number of assets to issue (i.e. an unlimited number of tokens can be issued for the custom asset), then you have the option of showing or hiding the tokens you issue during the issuance phase on the public block explorer.
*   `Transferability Type` - You can prevent your custom asset from being transferred to another user. This is an early feature that is designed to work with our upcoming timed lockup features.

    For example, in the future you will be able to set a custom asset as "non-transferrable" and specify a non-transferrable time period of 90 days — essentially creating a 90 day lockup to support a vesting schedule for the asset.

    * Click `Define New Asset` and then `Confirm` to complete this part of the process

    ![](https://wiki.findora.org/img/wallet/wallet23.png)

![](https://wiki.findora.org/img/wallet/wallet24.png)

1. Goto `Manage Assets` ⇒ `Issue Asset`
   * Fill out the input fields on the `Issue Asset` page

![wallet25.png](https://wiki.findora.org/assets/images/wallet25-0f46ed89eb6c3b20d0e148c9a9de2479.png)

* `Asset Creator` - select the wallet which created the custom asset
* `Asset Nickname` - select from the list of custom assets that have been previously defined
* `Issuance Amount` - enter the number of tokens to create. If the token was defined with a maximum units restriction, you will not be able to create tokens beyond the maximum limit.
* `Show or Hide Amounts on Ledger?` - choose whether the amounts will be shown or hidden for the assets to be issued
* Click `Confirm` to complete the process

![](https://wiki.findora.org/img/wallet/wallet26.png)

![](https://wiki.findora.org/img/wallet/wallet27.png)

### Manage Custom Assets[​](https://wiki.findora.org/docs/evm\_guides/use\_wallet/findora\_wallet/manage#manage-custom-assets) <a href="#manage-custom-assets" id="manage-custom-assets"></a>

* If you created your own custom assets earlier, you can manage these custom assets via the `Manage Assets` ⇒ `Manage` page

![wallet30.png](https://wiki.findora.org/assets/images/wallet30-2d8a0a1ab369f8e112ec066871260f65.png)

* Manage your custom assets via the following commands:
  * `Save` - saves _all_ custom asset data in the app to a text file on your computer. This data includes the asset code, nickname, wallet address that created asset, etc.)
  * `Open another file` - imports _all_ custom asset data saved in a text file on your computer
  * `+ Add` - imports a _single_ custom asset by manually inputting the relevant custom asset data
  * `Remove All` - removes all custom asset data from the app
