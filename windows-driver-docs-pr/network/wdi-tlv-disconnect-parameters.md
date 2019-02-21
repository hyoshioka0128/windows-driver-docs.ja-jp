---
title: WDI_TLV_DISCONNECT_PARAMETERS
description: WDI_TLV_DISCONNECT_PARAMETERS は、OID_WDI_TASK_DISCONNECT のパラメーターを含む TLV です。
ms.assetid: D0FF83A0-CD3B-47A6-BB08-842927F1D3BC
ms.date: 07/18/2017
keywords:
- WDI_TLV_DISCONNECT_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: d7c1fb88e0f9796207ff57ec23ff096ae1c1fdd1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552788"
---
# <a name="wditlvdisconnectparameters"></a>WDI\_TLV\_切断\_パラメーター


WDI\_TLV\_切断\_パラメーターはパラメーターを含む TLV [OID\_WDI\_タスク\_切断](https://msdn.microsoft.com/library/windows/hardware/dn925951)します。

## <a name="tlv-type"></a>TLV 型


0x36

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 種類                                              | 説明                                                                                                                                                                         |
|---------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_MAC\_アドレス**](https://msdn.microsoft.com/library/windows/hardware/dn926071) | 関連付けを解除するピアの MAC アドレス。                                                                                                                                        |
| UINT16                                            | ホストによってトリガーされる関連付け解除の理由です。 この値は、リトル エンディアン バイト順で提供される、送信の枠の理由コードに適切にコピーする必要があります。 |

 

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

 

 




