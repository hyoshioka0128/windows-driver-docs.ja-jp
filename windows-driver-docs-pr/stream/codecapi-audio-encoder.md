---
title: CODECAPI\_オーディオ\_エンコーダー
description: CODECAPI\_オーディオ\_エンコーダー
ms.assetid: c66cbbe1-36dc-4088-8ecd-7663d4503d6e
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71774812c89a4f093f6cf4498a3c55de501b8a36
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551722"
---
# <a name="codecapiaudioencoder"></a>CODECAPI\_オーディオ\_エンコーダー


## <span id="ddk_codecapi_audio_encoder_ks"></span><span id="DDK_CODECAPI_AUDIO_ENCODER_KS"></span>


オーディオ エンコーダーでは、この GUID (ユーザー モード KsProperty BASICSUPPORT でクエリを実行) のサポートを使用してオーディオ エンコーダーであることを示します。

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
<th>取得</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>〇</p></td>
<td><p>X</p></td>
<td><p>フィルター</p></td>
<td><p>KSPROPERTY</p></td>
<td><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (データの操作) は BOOL 型の、ミニドライバーがオーディオのエンコードをサポートしているかどうかを指定します。 値**TRUE**ミニドライバーは、オーディオのエンコードがサポートしていることを示します。 フィルターは、オーディオ エンコーダーではない場合、この GUID をサポートする必要があります。

### <a name="requirements"></a>要件

**ヘッダー:** 宣言されている*ksmedia.h*します。 含める*ksmedia.h*します。

### <a name="see-also"></a>参照

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

 

 





