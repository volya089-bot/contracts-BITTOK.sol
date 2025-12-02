// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

/*
 * BITTOK (BTITTOK)
 *  - Фіксована емісія: 21 000 000 BT
 *  - Дробність: 8 знаків після коми (як у Bitcoin)
 *  - Весь початковий запас отримує деплойер (msg.sender)
 *  - IPFS CID логотипа та метаданих зберігаються в публічних змінних
 */

import "https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.9.3/contracts/token/ERC20/ERC20.sol";
import "https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.9.3/contracts/access/Ownable.sol";

contract BITTOK is ERC20, Ownable {
    // ----- Параметри токена -----
    string public constant TOKEN_LOGO_CID =
        "bafybeidf4qrpdfpxttn3riohf5llx423vzzpunskfi4ckioisl3dsb32ue";
    string public constant TOKEN_METADATA_CID =
        "bafkreid2xrqoiqvt64kwupfxlcebuipudse3oikf7ximlf4scbcz7w2osa";

    // 8 знаків після коми (як у BTC)
    uint8 public constant DECIMALS = 8;

    // Загальна пропозиція: 21 000 000 * 10^8
    uint256 public constant MAX_SUPPLY = 21_000_000 * (10 ** DECIMALS);

    constructor() ERC20("BITTOK", "BITTOK") {
        // Власником стає деплойер контракту
        // (Ownable з OZ 4.9.3 сам встановлює msg.sender як owner)
        _mint(msg.sender, MAX_SUPPLY);
    }

    // Перевизначаємо decimals() під 8 знаків
    function decimals() public pure override returns (uint8) {
        return DECIMALS;
    }
}
