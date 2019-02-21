---
title: スマート カードの PC/SC インターフェイス
description: このトピックでは、各種 NFC カード ATR 形式について説明します。
ms.assetid: ''
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: bb96aa0d8dd80f0a478a9512b1eaef9e9a9b3ebf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551816"
---
# <a name="pcsc-interface-for-smart-cards"></a>スマート カードの PC/SC インターフェイス

各種 NFC カード ATR 形式は、以下に示します。 ATR 形式に関する詳細については、PC/SC 仕様 [3. a] を参照してください。

## <a name="atr-format-for-iso14443-4-cards"></a>ISO14443 4 のカードの ATR 形式

| バイト オフセット | Value | 指定      | 説明                                                                                                                 |
|-------------|-------|------------------|-----------------------------------------------------------------------------------------------------------------------------|
| 0           | 3B    | 初期ヘッダー   |                                                                                                                             |
| 1           | 8n    | T0               | 高いニブルでは、TD1 の存在のみを示します。 下のニブルが履歴のバイトのサイズを示します                       |
| 2           | 80    | TD1              | Presence of TD2                                                                                                             |
| 3           | 01    | TD2              |                                                                                                                             |
| 4 を 3 + N    | XX    | 履歴のバイト数 | ISO14443A:ATS 応答から履歴のバイトは、します。 <br> ISO14443B:履歴のバイトが ATTRIB (ATQB) |
| 4+N         | XX    | TCK              | チェックサム                                                                                                                    |

## <a name="atr-format-for-storage-cards"></a>メモリ カードの ATR 形式
<table>
    <tbody>
        <tr>
            <th>バイト オフセット</th>
            <th>Value</th>
            <th>指定</th>
            <th>説明</th>
        </tr>
        <tr>
            <td>0</td>
            <td>3B</td>
            <td>初期ヘッダー</td>
        </tr>
        <tr>
            <td>1</td>
            <td>8n</td>
            <td>T0</td>
            <td>高いニブルでは、TD1 の存在のみを示します。 下のニブルでは、履歴のバイトのサイズを示します。</td>
        </tr>
        <tr>
            <td>2</td>
            <td>80</td>
            <td>TD1</td>
            <td>Presence of TD2</td>
        </tr>
        <tr>
            <td>3</td>
            <td>01</td>
            <td>TD2</td>
        </tr>
        <tr>
            <td>4 を 3 + N</td>
            <td>80</td>
            <td>T1</td>
            <td>カテゴリのインジケーターのバイト。</td>
        </tr>
        <tr>
            <td>4 を 3 + N</td>
            <td>4F</td>
            <td>TK</td>
            <td>アプリケーション識別子が存在します。</td>
        </tr>
        <tr>
            <td>4 を 3 + N</td>
            <td>0 の C</td>
            <td>TK</td>
            <td>長さ</td>
        </tr>
        <tr>
            <td>4 を 3 + N</td>
            <td>A0 00 00 03 06</td>
            <td>TK</td>
            <td>PC/SC から補足ドキュメントの第 3 部で指定されている RID します。</td>
        </tr>
        <tr>
            <td>4 を 3 + N</td>
            <td>SS</td>
            <td>TK</td>
            <td>標準のバイト。 値は、補足ドキュメントの表 2 に対応する必要があります。</td>
        </tr>
        <tr>
            <td>4 を 3 + N</td>
            <td>NN</td>
            <td>TK</td>
            <td>カードの名前のバイト数。 値は、補足ドキュメントの表 3 に対応する必要があります。</td>
        </tr>
        <tr>
            <td>4 を 3 + N</td>
            <td>00 00 00 00</td>
            <td>RFU</td>
            <td></td>
        </tr>
        <tr>
            <td>4+N</td>
            <td>XX</td>
            <td>TCK<td>
            <td>チェックの合計</td>
        </tr>
    </tbody>
</table>
