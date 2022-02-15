# AVOID SCAM TRICKS INSIDE SOILIDITY CONTRACT

To help other to DYOR about solidity smart contract.

## Table of contents

- [USING OLD CONTRACT](#using-old-contract)
- [MINT TOKEN](#mint-token)
- [PAUSE TRADE](#pause-trade)
- [REVERT SELL](#revert-sell)
- [BLACKLIST ADDRESS](#blacklist-address)
- [SET MAX TX AMOUNT](#set-max-tx-amount)

## USING OLD CONTRACT
- Kontrak ini sudah tua dan telah diperbaharui, project baru seharusnya sudah tidak lagi menggunakan versi ini
- Jika dalam kontrak menggunakan uniswapV1Router. Dapat ditemukan dengan cara mencari address yang berawalan `0x05`
- untuk kontrak V2 terbaru yg aman uniswapV2Router `0x10ed43c718714eb63d5aa57b78b54704e256024e`

## MINT TOKEN
- Proses mint seharusnya dilakukan sekali, namun jika ada proses mint setelahnya, dev bisa terus menambah jumlah token dalam walletnya sendiri.
- Perhatikan function yang dapat menambahkan amount token ke total Supply dan wallet.
- Biasanya dev akan menamai function dengan nama yang lain, agar tidak diketahui.

## PAUSE TRADE
- Proses ini akan dilakukan dev agar holder lain selain dia, tidak bisa transaksi jual/beli. Hanya address tertentu yang bisa.
```php
    function setSellStatus(bool enabled) external onlyOwner {
        pauseSell = enabled;
    }
```
- Selalu perhatikan requirement dalam function transfer, bisa jadi ada function lain yang menghalangi proses trade.
```php
    if(to == uniswapV2Pair && pauseSell == true && from != owner()) {
        revert();
    }
```

## REVERT SELL
- Proses ini bertujuan agar holder selain dev/owner tidak bisa menjual token.
- Perhatikan jika dalam kontrak yang compiler solidity 0.5.xx :
```php
    pragma solidity 0.5.17;
```
- Jika ada seperti ini, maka berindikasi project ini scam dan dapat menimbulkan error "TRANSFER_FROM_FAILED" saat menjual token :
```php
    function() external payable {
        revert();
    }
    function() external payable {
    }
```
- Jika compilter 0.6.xx, proses ini dapat diabaikan :
```php
    pragma solidity 0.6.0;
```

## BLACKLIST ADDRESS
- Proses ini bertujuan untuk membuat beberapa address tidak bisa bertransaksi. 
- Perhatikan function external dengan kata kunci blacklist
```php
    function blacklistUpdate(address user, bool value)
        public
        virtual
        onlyOwner
    {
        _blacklist[user] = value;
        emit BlacklistUpdated(user, value);
    }
```
```php
    function blacklistAddress(address account) public onlyOwner {
        blacklist[account] = true;
    }
```
## SET MAX TX AMOUNT
- Proses ini bertujuan agar holder hanya dapat membeli dan menjual token di bawah angka maksimal
- Ini dapat berpotensi scam jika terdapat function external untuk mengubah nilai max jual/beli
```php
    function setMaxBuyTransaction(uint256 _maxTxn) external onlyOwner {
        maxBuyTransactionAmount = _maxTxn * (10**18);
    }
    function setMaxSellTransaction(uint256 _maxTxn) external onlyOwner {
        maxSellTransactionAmount = _maxTxn * (10**18);
    }
```



Beberapa list lagi akan di update
- HUGE GASFEE
- FLEXIBLE TAX
- TOKEN LOCK BESIDE PINKLOCK