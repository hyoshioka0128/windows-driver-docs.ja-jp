---
title: KSPROPERTY\_VIDEODECODER\_状態
description: KSPROPERTY\_VIDEDECODER\_STATUS プロパティは、ビデオ デコーダーからステータス情報を取得します。 このプロパティを実装する必要があります。
ms.assetid: 1d8cb537-1d85-4536-bd75-33beea0f586d
keywords:
- KSPROPERTY_VIDEODECODER_STATUS ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEODECODER_STATUS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f4d3c124bd1227434ea93b5f04cb008178fc274
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574330"
---
# <a name="kspropertyvideodecoderstatus"></a>KSPROPERTY\_VIDEODECODER\_状態


KSPROPERTY\_VIDEDECODER\_STATUS プロパティは、ビデオ デコーダーからステータス情報を取得します。 このプロパティを実装する必要があります。

## <span id="ddk_ksproperty_videodecoder_status_ks"></span><span id="DDK_KSPROPERTY_VIDEODECODER_STATUS_KS"></span>


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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566061" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_STATUS_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566061)"><strong>KSPROPERTY_VIDEODECODER_STATUS_S</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566061" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_STATUS_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566061)"><strong>KSPROPERTY_VIDEODECODER_STATUS_S</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、KSPROPERTY\_VIDEODECODER\_状態\_構造を受信したアナログ信号内の行の数などのビデオのデコード デバイスの現在の状態を指定するかどうかと、シグナル ロックされています。

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

[**KSPROPERTY\_VIDEODECODER\_状態\_S**](https://msdn.microsoft.com/library/windows/hardware/ff566061)

 

 






