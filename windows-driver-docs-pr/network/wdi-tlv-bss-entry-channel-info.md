---
title: WDI_TLV_BSS_ENTRY_CHANNEL_INFO
description: WDI_TLV_BSS_ENTRY_CHANNEL_INFO は、BSS エントリ チャネル情報を含む TLV です。
ms.assetid: 01DA2EDA-2BE2-4E4F-AE5D-8E07EEF691FE
ms.date: 07/18/2017
keywords:
- WDI_TLV_BSS_ENTRY_CHANNEL_INFO ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 1ef1ce103cbc16074fe9aada4beda535cf04b15d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355206"
---
# <a name="wditlvbssentrychannelinfo"></a>WDI\_TLV\_BSS\_エントリ\_チャネル\_情報


WDI\_TLV\_BSS\_エントリ\_チャネル\_情報が BSS エントリ チャネル情報を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x3A

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 型                          | 説明                                                  |
|-------------------------------|--------------------------------------------------------------|
| WDI\_チャネル\_数 (UINT32) | ピアが検出された論理チャネルの数。 |
| UINT32                        | BSS エントリのバンドの ID。                               |

 

<a name="requirements"></a>要件
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

 

 




