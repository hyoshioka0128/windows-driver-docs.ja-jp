---
title: CODECAPI\_変更リスト
description: CODECAPI\_変更リスト
ms.assetid: c1b65350-32b9-4c94-a6d4-74cb9959d737
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dbc0fd0642dbfd5b17e116d14cca7b4ca67a16e2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530619"
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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561937" data-raw-source="[&lt;strong&gt;KSE_NODE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561937)"><strong>KSE_NODE</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561750" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561750)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

DirectShow フィルターと KsProxy の詳細については、次を参照してください。[カーネル ストリーミング プロキシ](https://msdn.microsoft.com/library/windows/hardware/ff560877)します。

ドライバーの使用、AVStream [ **KsGenerateEvents** ](https://msdn.microsoft.com/library/windows/hardware/ff562597)変更 Guid のリストを投稿します。

### <a name="see-also"></a>参照

[**KsGenerateEvents**](https://msdn.microsoft.com/library/windows/hardware/ff562597), [CODECAPI\_ALLSETTINGS](codecapi-allsettings.md), [CODECAPI\_SETALLDEFAULTS](codecapi-setalldefaults.md)

 

 





