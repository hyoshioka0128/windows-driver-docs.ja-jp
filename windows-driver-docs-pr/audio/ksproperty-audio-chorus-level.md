---
title: KSPROPERTY\_オーディオ\_コーラス\_レベル
description: KSPROPERTY\_オーディオ\_コーラス\_レベル プロパティは、コーラス レベルを指定します。 これはコーラス ノードのプロパティ (KSNODETYPE\_コーラス)。
ms.assetid: 80541b2c-0fb3-4306-8ed2-e524b5a4c113
keywords:
- KSPROPERTY_AUDIO_CHORUS_LEVEL オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_CHORUS_LEVEL
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e82e8ea110650f1583f72a2c6fc89c46de7713de
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553206"
---
# <a name="kspropertyaudiochoruslevel"></a>KSPROPERTY\_オーディオ\_コーラス\_レベル


KSPROPERTY\_オーディオ\_コーラス\_レベル プロパティは、コーラス レベルを指定します。 これはコーラス ノードのプロパティ ([**KSNODETYPE\_コーラス**](ksnodetype-chorus.md))。

## <span id="ddk_ksproperty_audio_chorus_level_ks"></span><span id="DDK_KSPROPERTY_AUDIO_CHORUS_LEVEL_KS"></span>


### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

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
<th align="left">取得</th>
<th align="left">設定</th>
<th align="left">対象</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>〇</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>フィルター</p></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff537143" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537143)"><strong>KSNODEPROPERTY</strong></a></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は ULONG 型で、コーラス レベルを指定します。 コーラス レベル値は 0 から 100 に線形範囲に従います\*(65536-1/65536) %。

-   0x00010000 の値は、100% を表します。

-   100 を表す値が 0 xffffffff\*(65536-1/65536) % です。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_オーディオ\_コーラス\_レベル プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

このプロパティは、取得とコーラス エコーのボリューム レベルの設定に使用されます。

コーラスは、わずかな遅延でサウンドを元のエコーおよびエコーの遅延を少し乗算によって作成される音声 2 倍の効果です。 詳細については、の説明を参照して、 **IDirectSoundFXChorus** Microsoft Windows SDK ドキュメントのインターフェイス。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**KSNODETYPE\_コーラス**](ksnodetype-chorus.md)

[**KSNODEPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff537143)

 

 






