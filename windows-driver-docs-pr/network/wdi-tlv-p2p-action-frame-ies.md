---
title: WDI_TLV_P2P_ACTION_FRAME_IES
description: WDI_TLV_P2P_ACTION_FRAME_IES では、アクション フレーム IEs を含む TLV です。
ms.assetid: 7F5DD866-AD7D-4E3E-B352-78FAE4AFD995
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_ACTION_FRAME_IES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: bd10a7237c03759fc6df127de245fd0a406b5cb8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331220"
---
# <a name="wditlvp2pactionframeies"></a>WDI\_TLV\_P2P\_アクション\_フレーム\_IES


WDI\_TLV\_P2P\_アクション\_フレーム\_IES アクション フレーム IEs を含む TLV は、します。

## <a name="tlv-type"></a>TLV 型


0x90

## <a name="length"></a>長さ


UINT8 の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 型      | 説明                                                                                  |
|-----------|----------------------------------------------------------------------------------------------|
| UINT8\[\] | リモート デバイスに送信される IEs のセットを指定する UINT8 要素の配列。 |

 

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最小のクライアント</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




