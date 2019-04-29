---
title: KSPROPERTY\_SYSAUDIO\_コンポーネント\_ID
description: KSPROPERTY\_SYSAUDIO\_コンポーネント\_ID プロパティは、指定した仮想のオーディオ デバイスで使用される wave レンダリング デバイスからコンポーネントの ID を取得します。
ms.assetid: ef4a940f-dfef-43ed-8895-d318fb603e5c
keywords:
- KSPROPERTY_SYSAUDIO_COMPONENT_ID オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_SYSAUDIO_COMPONENT_ID
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 105c56ec112d16e8a21e6a7375bdded796435936
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332624"
---
# <a name="kspropertysysaudiocomponentid"></a>KSPROPERTY\_SYSAUDIO\_コンポーネント\_ID


KSPROPERTY\_SYSAUDIO\_コンポーネント\_ID プロパティは、指定した仮想のオーディオ デバイスで使用される wave レンダリング デバイスからコンポーネントの ID を取得します。

## <span id="ddk_ksproperty_sysaudio_component_id_ks"></span><span id="DDK_KSPROPERTY_SYSAUDIO_COMPONENT_ID_KS"></span>


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
<td align="left"><p>X</p></td>
<td align="left"><p>フィルター</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564262" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564262)"><strong>KSPROPERTY</strong></a>+ ULONG</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561027" data-raw-source="[&lt;strong&gt;KSCOMPONENTID&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561027)"><strong>KSCOMPONENTID</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ記述子 (インスタンス データ) は、仮想のオーディオ デバイスを識別するデバイス ID を含む ULONG 変数を続けて KSPROPERTY 型の構造です。 SysAudio 列挙する場合*n*仮想のオーディオ デバイス (を参照してください[ **KSPROPERTY\_SYSAUDIO\_デバイス\_カウント**](ksproperty-sysaudio-device-count.md)) し、有効なデバイス Id の範囲は 0 ~ *n*-1。

プロパティの値 (データの操作) は、種類、製造元、製品、および、指定された仮想オーディオ デバイスによって使用される、wave レンダリング デバイスに関するその他のハードウェアに固有の情報を指定する KSCOMPONENTID の構造です。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_SYSAUDIO\_コンポーネント\_ID プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

DirectSound は、各 SysAudio の仮想のオーディオ デバイスを基になるオーディオ ハードウェアのミニポート ドライバーと直接通信しません。 したがって、DirectSound は、コンポーネント ID 情報を直接 wave レンダリング デバイスを照会することができません。 KSPROPERTY\_SYSAUDIO\_コンポーネント\_ID プロパティは DirectSound SysAudio を通じて間接的にこの情報を取得するための手段を提供します。

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


[**KSPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff564262)

[**KSCOMPONENTID**](https://msdn.microsoft.com/library/windows/hardware/ff561027)

[**KSPROPERTY\_SYSAUDIO\_デバイス\_数**](ksproperty-sysaudio-device-count.md)

 

 






