---
title: CODECAPI\_AUDIO\_ENCODER
description: CODECAPI\_AUDIO\_ENCODER
ms.assetid: c66cbbe1-36dc-4088-8ecd-7663d4503d6e
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef9f7774d0c85f8c0296993a9b6dfbe6d08520fa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844729"
---
# <a name="codecapi_audio_encoder"></a>CODECAPI\_AUDIO\_ENCODER


## <span id="ddk_codecapi_audio_encoder_ks"></span><span id="DDK_CODECAPI_AUDIO_ENCODER_KS"></span>


オーディオエンコーダーは、この GUID のサポート (ユーザーモード KsProperty BASICSUPPORT によって照会されます) を使用して、オーディオエンコーダーであることを示します。

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

 

プロパティ値 (操作データ) はブール型で、ミニドライバーがオーディオエンコーディングをサポートするかどうかを指定します。 値が**TRUE の場合**は、ミニドライバーがオーディオエンコーディングをサポートしていることを示します。 この GUID がオーディオエンコーダーではない場合は、フィルターでサポートしないでください。

### <a name="requirements"></a>要件

**ヘッダー:** *Ksmedia. h*で宣言されています。 *Ksmedia. h*をインクルードします。

### <a name="see-also"></a>参照

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

 

 





