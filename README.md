# AVOID SCAM TRICKS INSIDE SOILIDITY CONTRACT

To help other to DYOR about solidity smart contract.

1. USING V1 BROKEN CONTRACT

    Kontrak ini sudah tua dan telah diperbaharui, project baru seharusnya sudah tidak lagi menggunakan versi ini.
    Jika dalam kontrak menggunakan uniswapV1Router. Dapat ditemukan dengan cara mencari address yang berawalan "0x05".
    untuk kontrak V2 terbaru yg aman uniswapV2Router : 0x10ed43c718714eb63d5aa57b78b54704e256024e

2. MINT TOKEN

    Proses mint seharusnya dilakukan sekali, namun jika ada proses mint setelahnya, dev bisa terus menambah jumlah token dalam walletnya sendiri.
    Perhatikan function yang dapat menambahkan amount token ke total Supply dan wallet.
    Biasanya dev akan menamai function dengan nama yang lain, agar tidak diketahui.

3. PAUSE TRADE

    Proses ini akan dilakukan dev agar holder lain selain dia, tidak bisa transaksi jual/beli. Hanya address tertentu yang bisa.
    Selalu perhatikan requirement dalam function transfer, bisa jadi ada function lain yang menghalangi proses trade.

4. REVERT SELL

    Proses ini bertujuan agar holder selain dev/owner tidak bisa menjual token.
    Perhatikan jika dalam kontrak yang compiler solidity 0.5.xx :

    ```php
        pragma solidity 0.5.17;
    ```

    ada seperti ini, maka berindikasi project ini scam dan dapat menimbulkan error "TRANSFER_FROM_FAILED" saat menjual token :

    ```php
    function() external payable {
        revert();
    }
    function() external payable {
    }
    ```

    jika compilter 0.6.xx, proses ini dapat diabaikan :

    ```php
        pragma solidity 0.6.0;
    ```

5. BLACKLIST ADDRESS

    Proses ini bertujuan untuk membuat beberapa address tidak bisa bertransaksi. Perhatikan function external dengan kata kunci blacklist

Beberapa list lagi akan di update

- HUGE GASFEE
- FLEXIBLE TAX
- SET MAX TX AMOUNT
- TOKEN LOCK BESIDE PINKLOCK