---
title: WDI_TLV_INCOMING_ASSOCIATION_REQUEST_PARAMETERS
description: WDI_TLV_INCOMING_ASSOCIATION_REQUEST_PARAMETERS では、アソシエーションの要求パラメーターを含む TLV です。
ms.assetid: DC3439A2-2221-4489-AB38-3752624EA4B2
ms.date: 07/18/2017
keywords:
- WDI_TLV_INCOMING_ASSOCIATION_REQUEST_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: ee261a46dc34faa5b06b3858f371991b73a671f7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574366"
---
# <a name="wditlvincomingassociationrequestparameters"></a>WDI\_TLV\_受信\_アソシエーション\_要求\_パラメーター


WDI\_TLV\_受信\_アソシエーション\_要求\_パラメーターは、アソシエーションの要求パラメーターを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x7D

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 型                                              | 説明                                                                                                                   |
|---------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_MAC\_アドレス**](https://msdn.microsoft.com/library/windows/hardware/dn926071) | 送信者の MAC アドレス。                                                                                                |
| UINT8                                             | これは、再関連付け要求かどうかを示すビット。 1 の値では、再関連付け要求であることを示します。 |

 

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

 

 




