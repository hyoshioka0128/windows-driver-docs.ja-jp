---
title: CODECAPI\_SUPPORTSEVENTS
description: CODECAPI\_SUPPORTSEVENTS
ms.assetid: feb6d110-9a9c-4e2b-bc19-259f80f3947a
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3add63d9a6c4d1be086762aff919358a7f7fa00e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528954"
---
# <a name="codecapisupportsevents"></a>CODECAPI\_SUPPORTSEVENTS


## <span id="ddk_codecapi_supportsevents_ks"></span><span id="DDK_CODECAPI_SUPPORTSEVENTS_KS"></span>


CODECAPI\_SUPPORTSEVENTS プロパティは、ミニドライバーはユーザー モード イベントをサポートするかどうかを示すために使用します。 つまり、ミニドライバーを実装して、 [CODECAPI\_変更リスト](codecapi-changelists.md)イベント。

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
<td><p>〇</p></td>
<td><p>フィルター</p></td>
<td><p>KSPROPERTY</p></td>
<td><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (データの操作)、ミニドライバーはユーザー モード イベントをサポートするかどうかを指定するブール値の型です。 値**TRUE**ミニドライバーのサポートを提供することを示します。 ミニドライバーは、イベント メカニズムがサポートしない場合、この GUID をサポートされていませんする必要があります。

### <a name="requirements"></a>要件

**ヘッダー:** 宣言されている*ksmedia.h*します。 含める*ksmedia.h*します。

### <a name="see-also"></a>参照

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

 

 





