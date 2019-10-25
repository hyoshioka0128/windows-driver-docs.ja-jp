---
title: CODECAPI\_CHANGELISTS
description: CODECAPI\_CHANGELISTS
ms.assetid: c1b65350-32b9-4c94-a6d4-74cb9959d737
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02d770e17b22135ab72a5f285c4d42e4d7c2a6b1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844727"
---
# <a name="codecapi_changelists"></a>CODECAPI\_CHANGELISTS


## <span id="ddk_codecapi_changelists_ks"></span><span id="DDK_CODECAPI_CHANGELISTS_KS"></span>


CODECAPI\_CHANGELISTS イベントを使用して、 [CODECAPI\_ALLSETTINGS](codecapi-allsettings.md)および[CODECAPI\_setalldefaults](codecapi-setalldefaults.md)、encoder setting プロパティなどのプロパティ "set" 呼び出しの結果として変更された guid の一覧を返します。

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
<th>イベント記述子の種類</th>
<th>イベント値の種類</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>はい (クエリはサポートされています)</p></td>
<td><p>[はい]</p></td>
<td><p>フィルター</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kse_node" data-raw-source="[&lt;strong&gt;KSE_NODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kse_node)"><strong>KSE_NODE</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

DirectShow フィルターと Ksk プロキシの詳細については、「[カーネルストリーミングプロキシ](https://docs.microsoft.com/windows-hardware/drivers/ddi/_stream/index)」を参照してください。

ドライバーは、AVStream [**Ksgenerateevents**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksgenerateevents)を使用して、変更された guid の一覧をポストします。

### <a name="see-also"></a>参照

[**Ksgenerateevents**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksgenerateevents)、 [CODECAPI\_allsettings](codecapi-allsettings.md)、 [CODECAPI\_setalldefaults](codecapi-setalldefaults.md)

 

 





