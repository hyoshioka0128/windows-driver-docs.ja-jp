---
title: CODECAPI\_ビデオ\_エンコーダー
description: CODECAPI\_ビデオ\_エンコーダー
ms.assetid: e08f26ff-1e11-42a4-a9f8-3af9b885a901
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85c5984822ce79b91000dba0eadff1fdefd9b5cb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329592"
---
# <a name="codecapivideoencoder"></a>CODECAPI\_ビデオ\_エンコーダー


## <span id="ddk_codecapi_video_encoder_ks"></span><span id="DDK_CODECAPI_VIDEO_ENCODER_KS"></span>


ビデオ エンコーダーでは、この GUID (ユーザー モード KsProperty BASICSUPPORT でクエリを実行) のサポートを使用しているビデオ エンコーダーを指定します。

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

 

プロパティ値 (データの操作) は BOOL 型のビデオ エンコード、ミニドライバーをサポートするかどうかを指定します。 値**TRUE**ミニドライバーは、ビデオ エンコードがサポートしていることを示します。 フィルターは、ビデオ エンコーダーではない場合、この GUID をサポートする必要があります。

### <a name="span-idheadersspanspan-idheadersspanheaders"></a><span id="headers"></span><span id="HEADERS"></span>ヘッダー

宣言されている*ksmedia.h*します。 含める*ksmedia.h*します。

### <a name="requirements"></a>要件

**ヘッダー:** 宣言されている*ksmedia.h*します。 含める*ksmedia.h*します。

### <a name="see-also"></a>関連項目

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

 

 





