---
title: KSPROPERTY\_SYSAUDIO\_デバイス\_インスタンス
description: KSPROPERTY\_SYSAUDIO\_デバイス\_インスタンス プロパティが仮想のオーディオ デバイスの現在のインスタンスを指定します。
ms.assetid: 67cdc1ec-c696-454f-a3cc-1b50418c4056
keywords:
- KSPROPERTY_SYSAUDIO_DEVICE_INSTANCE オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_SYSAUDIO_DEVICE_INSTANCE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad62b92d832c5b448869f5f53599483ff13787d3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558659"
---
# <a name="kspropertysysaudiodeviceinstance"></a>KSPROPERTY\_SYSAUDIO\_デバイス\_インスタンス


KSPROPERTY\_SYSAUDIO\_デバイス\_インスタンス プロパティが仮想のオーディオ デバイスの現在のインスタンスを指定します。

## <span id="ddk_ksproperty_sysaudio_device_instance_ks"></span><span id="DDK_KSPROPERTY_SYSAUDIO_DEVICE_INSTANCE_KS"></span>


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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564262" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564262)"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は ULONG 型で、仮想のオーディオ デバイスのデバイス ID を指定します。 SysAudio 列挙する場合*n*仮想のオーディオ デバイス (を参照してください[ **KSPROPERTY\_SYSAUDIO\_デバイス\_カウント**](ksproperty-sysaudio-device-count.md)) し、有効なデバイス Id の範囲は 0 ~ *n*-1。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_SYSAUDIO\_デバイス\_インスタンス プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

KSPROPERTY\_SYSAUDIO\_デバイス\_インスタンス プロパティの設定要求は、プロパティの値に含まれるデバイス ID で指定された仮想オーディオ デバイスを開きます。 最後に開かれるデバイスは、現在のデバイスと呼ばれます。

いくつかの SysAudio プロパティに 0 の範囲の有効なデバイス ID ではなく-1 の null デバイス ID で識別する現在のデバイスを許可する*n*-1 の場合、 *n*は使用可能な仮想オーディオ デバイスの数です。 これらのプロパティを含める[ **KSPROPERTY\_SYSAUDIO\_デバイス\_インターフェイス\_名前**](ksproperty-sysaudio-device-interface-name.md)と[ **KSPROPERTY\_SYSAUDIO\_デバイス\_フレンドリ\_名前**](ksproperty-sysaudio-device-friendly-name.md)します。

Get プロパティは、デバイス ID を取得します (最後に開かれた) 現在の仮想のオーディオ デバイスを要求します。

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

[**KSPROPERTY\_SYSAUDIO\_デバイス\_数**](ksproperty-sysaudio-device-count.md)

[**KSPROPERTY\_SYSAUDIO\_デバイス\_インターフェイス\_名**](ksproperty-sysaudio-device-interface-name.md)

[**KSPROPERTY\_SYSAUDIO\_デバイス\_フレンドリ\_名**](ksproperty-sysaudio-device-friendly-name.md)

 

 






