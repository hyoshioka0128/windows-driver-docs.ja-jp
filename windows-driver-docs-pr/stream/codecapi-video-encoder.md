---
title: CODECAPI\_VIDEO\_ENCODER
description: CODECAPI\_VIDEO\_ENCODER
ms.assetid: e08f26ff-1e11-42a4-a9f8-3af9b885a901
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b75814fd9dbdeccb9a9702a2873129c96b020e9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844719"
---
# <a name="codecapi_video_encoder"></a>CODECAPI\_VIDEO\_ENCODER


## <span id="ddk_codecapi_video_encoder_ks"></span><span id="DDK_CODECAPI_VIDEO_ENCODER_KS"></span>


ビデオエンコーダーは、この GUID のサポート (ユーザーモード KsProperty BASICSUPPORT によって照会されます) を使用して、それらがビデオエンコーダーであることを示します。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>[購入]</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>[はい]</p></td>
<td><p>必須ではない</p></td>
<td><p>フィルター</p></td>
<td><p>KSPROPERTY</p></td>
<td><p>型</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) はブール型で、ミニドライバーがビデオエンコーディングをサポートするかどうかを指定します。 値が**TRUE の場合**は、ミニドライバーがビデオエンコーディングをサポートしていることを示します。 この GUID がビデオエンコーダーでない場合は、フィルターでサポートしないでください。

### <a name="span-idheadersspanspan-idheadersspanheaders"></a><span id="headers"></span><span id="HEADERS"></span>ヘッダー

*Ksmedia. h*で宣言されています。 *Ksmedia. h*をインクルードします。

### <a name="requirements"></a>要件

**ヘッダー:** *Ksmedia. h*で宣言されています。 *Ksmedia. h*をインクルードします。

### <a name="see-also"></a>参照

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

 

 





