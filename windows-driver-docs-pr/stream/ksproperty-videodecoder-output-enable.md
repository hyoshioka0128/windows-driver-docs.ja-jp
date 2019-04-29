---
title: KSPROPERTY\_VIDEODECODER\_出力\_を有効にします。
description: KSPROPERTY\_VIDEODECODER\_出力\_有効にするプロパティは、ビデオ ポートを共有バス上に存在するビデオ デコーダーの 3 つの状態の出力を制御します。 このプロパティは省略可能です。
ms.assetid: 33c9a3d2-ffc0-4460-abc4-56bc83c64b55
keywords:
- KSPROPERTY_VIDEODECODER_OUTPUT_ENABLE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEODECODER_OUTPUT_ENABLE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b8d86f384112e86446b9223543b765e5431644d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325984"
---
# <a name="kspropertyvideodecoderoutputenable"></a>KSPROPERTY\_VIDEODECODER\_出力\_を有効にします。


KSPROPERTY\_VIDEODECODER\_出力\_有効にするプロパティは、ビデオ ポートを共有バス上に存在するビデオ デコーダーの 3 つの状態の出力を制御します。 このプロパティは省略可能です。

## <span id="ddk_ksproperty_videodecoder_output_enable_ks"></span><span id="DDK_KSPROPERTY_VIDEODECODER_OUTPUT_ENABLE_KS"></span>


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
<td><p>Pin</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566052" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566052)"><strong>KSPROPERTY_VIDEODECODER_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、設定する 3 つの状態の出力を有効にするを指定する ULONG です。 ゼロの値では、3 つの状態の出力を示します。 0 以外の値は、デバイスのビデオ ポート バスがアクティブに生じていることを示します。

<a name="remarks"></a>注釈
-------

**値**、KSPROPERTY のメンバー\_VIDEODECODER\_の構造は、3 つの出力を有効にする 設定を指定します。

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

[**KSPROPERTY\_VIDEODECODER\_S**](https://msdn.microsoft.com/library/windows/hardware/ff566052)

 

 






