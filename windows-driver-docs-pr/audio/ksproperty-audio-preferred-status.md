---
title: KSK プロパティ\_オーディオ\_優先\_状態
description: KSK プロパティ\_AUDIO\_優先\_状態プロパティは、システムの優先オーディオデバイスであることをデバイスに通知します。
ms.assetid: a0e89143-ead1-4e0d-a550-398ec1abf9e9
keywords:
- KSPROPERTY_AUDIO_PREFERRED_STATUS オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_PREFERRED_STATUS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 13ab53cee6091120320c1282aeb7df32c7147e9b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830941"
---
# <a name="ksproperty_audio_preferred_status"></a>KSK プロパティ\_オーディオ\_優先\_状態


KSK プロパティ\_AUDIO\_優先\_状態プロパティは、システムの優先オーディオデバイスであることをデバイスに通知します。

## <span id="ddk_ksproperty_audio_preferred_status_ks"></span><span id="DDK_KSPROPERTY_AUDIO_PREFERRED_STATUS_KS"></span>


### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

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
<th align="left">[購入]</th>
<th align="left">設定</th>
<th align="left">対象</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>必須ではない</p></td>
<td align="left"><p>[はい]</p></td>
<td align="left"><p>フィルター</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_preferred_status" data-raw-source="[&lt;strong&gt;KSAUDIO_PREFERRED_STATUS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_preferred_status)"><strong>KSAUDIO_PREFERRED_STATUS</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、"KSAUDIO\_\_型の構造であり、優先されるデバイスの種類を指定し、デバイスを選択するか、デバイスの種類に適したデバイスとして選択するかを選択します。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_AUDIO\_好ましい\_STATUS プロパティ要求は、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

[Sysaudio システムドライバー](https://docs.microsoft.com/windows-hardware/drivers/audio/kernel-mode-wdm-audio-components#sysaudio-system-driver)は、このプロパティを使用して、新しい優先デバイスとして選択されたとき、または選択された優先デバイスが選択解除されたときに、wave 再生、wave レコード、MIDI、またはミキサーデバイスに通知します。

優先されるデバイスの詳細については、「 [**Setuppreferredaudiodevices**](setuppreferredaudiodevices.md)」を参照してください。

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
<td align="left">Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))

[**KSAUDIO\_優先\_ステータス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_preferred_status)

[**SetupPreferredAudioDevices**](setuppreferredaudiodevices.md)

 

 






