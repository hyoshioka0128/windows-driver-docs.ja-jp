---
title: CODECAPI\_SUPPORTSEVENTS
description: CODECAPI\_SUPPORTSEVENTS
ms.assetid: feb6d110-9a9c-4e2b-bc19-259f80f3947a
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 127775d01129a6f2f79df412ae62d6d30ebbcbdb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844722"
---
# <a name="codecapi_supportsevents"></a>CODECAPI\_SUPPORTSEVENTS


## <span id="ddk_codecapi_supportsevents_ks"></span><span id="DDK_CODECAPI_SUPPORTSEVENTS_KS"></span>


CODECAPI\_SUPPORTSEVENTS プロパティは、ミニドライバーがユーザーモードイベントをサポートするかどうかを示すために使用されます。 つまり、ミニドライバーは、 [CODECAPI\_CHANGELISTS](codecapi-changelists.md)イベントを実装します。

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
<td><p>[はい]</p></td>
<td><p>フィルター</p></td>
<td><p>KSPROPERTY</p></td>
<td><p>型</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、ミニドライバーがユーザーモードイベントをサポートするかどうかを指定するブール型です。 値が**TRUE の場合**は、ミニドライバーによってサポートが提供されることを示します。 イベントメカニズムがサポートされていない場合、ミニドライバーはこの GUID をサポートしません。

### <a name="requirements"></a>要件

**ヘッダー:** *Ksmedia. h*で宣言されています。 *Ksmedia. h*をインクルードします。

### <a name="see-also"></a>参照

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

 

 





