---
title: CODECAPI\_変更リスト
description: CODECAPI\_変更リスト
ms.assetid: c1b65350-32b9-4c94-a6d4-74cb9959d737
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: be21fad3cd401a0cab02b8745f48905c15d72437
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386649"
---
# <a name="codecapichangelists"></a>CODECAPI\_変更リスト


## <span id="ddk_codecapi_changelists_ks"></span><span id="DDK_CODECAPI_CHANGELISTS_KS"></span>


CODECAPI\_変更リスト イベントは、プロパティの結果として変更された Guid のリスト「などの設定」の呼び出し、返される使用[CODECAPI\_ALLSETTINGS](codecapi-allsettings.md)と[CODECAPI\_SETALLDEFAULTS](codecapi-setalldefaults.md)エンコーダーは、プロパティを設定します。

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
<th>イベント記述子の種類</th>
<th>イベント値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>[はい] (クエリがサポートされています)</p></td>
<td><p>〇</p></td>
<td><p>フィルター</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kse_node" data-raw-source="[&lt;strong&gt;KSE_NODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kse_node)"><strong>KSE_NODE</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kseventdata" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kseventdata)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

DirectShow フィルターと KsProxy の詳細については、次を参照してください。[カーネル ストリーミング プロキシ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_stream/index)します。

ドライバーの使用、AVStream [ **KsGenerateEvents** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksgenerateevents)変更 Guid のリストを投稿します。

### <a name="see-also"></a>参照

[**KsGenerateEvents**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksgenerateevents), [CODECAPI\_ALLSETTINGS](codecapi-allsettings.md), [CODECAPI\_SETALLDEFAULTS](codecapi-setalldefaults.md)

 

 





