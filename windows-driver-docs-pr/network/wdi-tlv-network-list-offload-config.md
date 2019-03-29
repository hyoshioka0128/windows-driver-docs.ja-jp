---
title: WDI_TLV_NETWORK_LIST_OFFLOAD_CONFIG
description: WDI_TLV_NETWORK_LIST_OFFLOAD_CONFIG では、ネットワークの一覧のオフロード (NLO) 構成を含む TLV です。
ms.assetid: 8805B31C-7601-4045-AD52-21B91E2D3722
ms.date: 07/18/2017
keywords:
- WDI_TLV_NETWORK_LIST_OFFLOAD_CONFIG ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 661e49bac0106242b6c533fac5d3209c50567071
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574619"
---
# <a name="wditlvnetworklistoffloadconfig"></a>WDI\_TLV\_ネットワーク\_一覧\_オフロード\_構成


WDI\_TLV\_ネットワーク\_一覧\_オフロード\_構成は、ネットワークの一覧のオフロード (NLO) 構成を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0xDA

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 型   | 説明                                                                                                           |
|--------|-----------------------------------------------------------------------------------------------------------------------|
| UINT32 | 予約フィールドです。                                                                                                       |
| UINT32 | スキャンのスケジュールの待ち時間を秒単位で開始します。                                                               |
| UINT32 | 秒単位で期間を最初のフェーズでスキャンします。                                                                   |
| UINT32 | 高速スキャン フェーズでのイテレーションの数。                                                                      |
| UINT32 | 秒単位で期間を低速スキャン フェーズでスキャンします。 このフェーズは、新しい NLO コマンドが設定されるまで無期限に続きます。 |

 

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

 

 




