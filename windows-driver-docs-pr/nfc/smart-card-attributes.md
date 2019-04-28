---
title: サポートされているスマート カードの属性
description: このトピックでは、サポートされているスマート カードの属性について説明します。
ms.assetid: ''
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8fbb292ea7c4e3e1bb5f60dc89d89b2e37e67dd8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373695"
---
# <a name="supported-smart-card-attributes"></a>サポートされているスマート カードの属性
このトピックでは、現在サポートされているスマート カードの属性について説明します。 以下に示します。 サポートされている属性のみが表示されています。STATUS_NOT_SUPPORTED として、Winsmcrd.h で定義されている他のすべての属性が返されます。 属性は「 *ICCs およびパーソナル コンピューター システムの相互運用性の仕様*します。

<table>
    <tbody>
        <tr>
            <th>属性タグ</th>
            <th>説明</th>
        </tr>
        <tr>
            <td>CARD_ATTR_CURRENT_PROTOCOL_TYPE</td>
            <td>SCARD_PROTOCOL_T1</td>
        </tr>
        <tr>
            <td>SCARD_ATTR_CURRENT_CLK</td>
            <td>13560 (13.56 mhz 以上のリトル エンディアンの整数)</td>
        </tr>
        <tr>
            <td>SCARD_ATTR_CURRENT_D</td>
            <td>1</td>
        </tr>
        <tr>
            <td>SCARD_ATTR_CURRENT_IFSC</td>
            <td>32</td>
        </tr>
        <tr>
            <td>SCARD_ATTR_CURRENT_IFSD</td>
            <td>254</td>
        </tr>
        <tr>
            <td>SCARD_ATTR_CURRENT_BWT</td>
            <td>4</td>
        </tr>
        <tr>
            <td>SCARD_ATTR_DEFAULT_CLK</td>
            <td>13560</td>
        </tr>
        <tr>
            <td>SCARD_ATTR_MAX_CLK</td>
            <td>13560</td>
        </tr>
        <tr>
            <td>SCARD_ATTR_DEFAULT_DATA_RATE</td>
            <td>1</td>
        </tr>
        <tr>
            <td>SCARD_ATTR_MAX_DATA_RATE</td>
            <td>1</td>
        </tr>
        <tr>
            <td>SCARD_ATTR_CHARACTERISTICS</td>
            <td>SCARD_READER_CONTACTLESS</td>
        </tr>
        <tr>
            <td>SCARD_ATTR_MAX_IFSD</td>
            <td>254</td>
        </tr>
        <tr>
            <td>SCARD_ATTR_VENDOR_NAME</td>
            <td>ASCII の string</td>
        </tr>
        <tr>
            <td>SCARD_ATTR_VENDOR_IFD_TYPE</td>
            <td>ASCII の string</td>
        </tr>
        <tr>
            <td>SCARD_ATTR_VENDOR_IFD_VERSION</td>
            <td>0x01000010、バージョン 1.0.0.1</td>
        </tr>
        <tr>
            <td>SCARD_ATTR_PROTOCOL_TYPES</td>
            <td>SCARD_PROTOCOL_T1</td>
        </tr>
        <tr>
            <td>SCARD_ATTR_DEVICE_UNIT</td>
            <td>0</td>
        </tr>
        <tr>
            <td>SCARD_ATTR_CHANNEL_ID</td>
            <td>
DWORD 0xDDDDCCCC、DDDD はデータ チャネルの種類、CCCC がチャンネル番号としてエンコードします。 DDDD では、次のエンコードが定義されます。 <table>
                    <tbody>
                        <tr>
                            <th>データ チャネル (DDDD)</th>
                            <th>種類</th>
                            <th>チャンネル番号 (CCCC)</th>
                        </tr>
                        <tr>
                            <td>0x0100</td>
                            <td>NFC</td>
                            <td>0</td>
                        </tr>
                        <tr>
                            <td>0x0200</td>
                            <td>UICC</td>
                            <td>0</td>
                        </tr>
                        <tr>
                            <td>0x0800</td>
                            <td>埋め込み SE</td>
                            <td>0</td>
                        </tr>
                        <tr>
                            <td>0xFXXX</td>
                            <td>ベンダ定義のチャネルの種類</td>
                            <td>ベンダー定義</td>
                        </tr><br/>                    </tbody>
                </table>
            </td>
        </tr>
    <tbody>
</table>

## <a name="icc-attributes"></a>ICC 属性

<table>
    <tbody>
        <tr>
            <th>属性タグ</th>
            <th>説明</th>
        </tr>
        <tr>
            <td>SCARD_ATTR_ICC_PRESENCE</td>
            <td>(1 バイト) <ul>
                    <li> 0 = 存在しません </li>
                    <li> 1 = カード</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>SCARD_ATTR_ATR_STRING</td>
            <td>(32 バイト) <ul>
                    <li> ATR 文字列 </li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>SCARD_ATTR_ICC_TYPE_PER_ATR</td>
            <td>(1 バイト) <ul>
                    <li> 0 = 不明な型 </li>
                    <li> 5 = 14443A </li>
                    <li> 6 = 14443B </li>
                    <li> 7 = ISO 15693 </li>
                </ul>
            </td>
        </tr>
