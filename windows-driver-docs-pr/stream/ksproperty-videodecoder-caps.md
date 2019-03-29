---
title: KSPROPERTY\_VIDEODECODER\_キャップ
description: KSPROPERTY\_VIDEODECODER\_CAPS プロパティがビデオ デコーダーの基本的な機能について説明します。 このプロパティを実装する必要があります。
ms.assetid: 8b252f36-911b-4f51-894d-3aae9aa9dfde
keywords:
- KSPROPERTY_VIDEODECODER_CAPS ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEODECODER_CAPS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 812fe7b48158ab571c8f1c8fdbcb5109f7f2590c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572340"
---
# <a name="kspropertyvideodecodercaps"></a>KSPROPERTY\_VIDEODECODER\_キャップ


KSPROPERTY\_VIDEODECODER\_CAPS プロパティがビデオ デコーダーの基本的な機能について説明します。 このプロパティを実装する必要があります。

## <span id="ddk_ksproperty_videodecoder_caps_ks"></span><span id="DDK_KSPROPERTY_VIDEODECODER_CAPS_KS"></span>


### <a name="usage-summary-table"></a>使用状況の概要テーブル

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
<th>Set</th>
<th>移行先</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>はい</p></td>
<td><p>いいえ</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566047" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_CAPS_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566047)"><strong>KSPROPERTY_VIDEODECODER_CAPS_S</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566047" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_CAPS_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566047)"><strong>KSPROPERTY_VIDEODECODER_CAPS_S</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、KSPROPERTY\_VIDEODECODER\_CAP\_構造など、ビデオ デコーダー デバイスのハードウェア機能を指定するには、時刻、および水平方向の決済標準がサポートされていますビデオ デコーダーが垂直方向の同期の期間中に生成パルスを同期します。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_VIDEODECODER\_CAP\_S**](https://msdn.microsoft.com/library/windows/hardware/ff566047)

 

 






