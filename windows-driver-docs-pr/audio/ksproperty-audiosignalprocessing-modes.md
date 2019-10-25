---
title: KSK プロパティ\_AUDIOSIGNALPROCESSING\_モード
description: KSK プロパティ\_AUDIOSIGNALPROCESSING\_MODES プロパティは、ピンファクトリによってサポートされるオーディオシグナル処理モードの一覧を返します。
ms.assetid: 95536F80-D4E0-48CB-8DB2-603C4CEF0053
keywords:
- KSPROPERTY_AUDIOSIGNALPROCESSING_MODES オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIOSIGNALPROCESSING_MODES
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06957e2014e3cb50f0d3a44b5d816cbaeea1c66e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830845"
---
# <a name="ksproperty_audiosignalprocessing_modes"></a>KSK プロパティ\_AUDIOSIGNALPROCESSING\_モード


**Ksk プロパティ\_AUDIOSIGNALPROCESSING\_MODES**プロパティは、ピンファクトリによってサポートされるオーディオシグナル処理モードの一覧を返します。

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
<td align="left"><p>[はい]</p></td>
<td align="left"><p>必須ではない</p></td>
<td align="left"><p>Pin ファクトリ (フィルターインスタンス経由)</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin" data-raw-source="[KSP_PIN](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)">KSP_PIN</a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item" data-raw-source="[KSMULTIPLE_ITEM](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)">KSMULTIPLE_ITEM</a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値は構造体であり、その後にゼロ (0) 以上の Guid が続きます。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

**Ksk プロパティ\_AUDIOSIGNALPROCESSING\_モード**では、 **KSPROPERTY\_項目**の後に 0 (0) 以上の guid が続く値が返されます。 KSMULTIPLE\_項目。Count メンバーには、Guid の数が含まれます。 KSMULTIPLE\_項目。Size メンバーには、プロパティ値の合計サイズが含まれます。 各 GUID は、 **KSP\_pin**構造体の*pinid*メンバーに指定されている pin id に対して、オーディオドライバーによってサポートされるシグナル処理モードを識別します。

Windows 8.1 オーディオ信号処理モードが2つ定義されていましたが、AUDIO\_SIGNALPROCESSINGMODE\_DEFAULT と AUDIO\_SIGNALPROCESSINGMODE\_RAW になっていました。

Windows 10 では、追加のモードが5つ定義されています。

AUDIO\_SIGNALPROCESSINGMODE\_COMMUNICATIONS AUDIO\_SIGNALPROCESSINGMODE\_SPEECH AUDIO\_SIGNALPROCESSINGMODE\_MEDIA AUDIO\_SIGNALPROCESSINGMODE\_MOVIE AUDIO\_SIGNALPROCESSINGMODE\_通知の詳細については、「[オーディオ信号処理モード](https://docs.microsoft.com/windows-hardware/drivers/audio/audio-signal-processing-modes)」を参照してください。

<a name="remarks"></a>注釈
-------

**Ksk プロパティ\_AUDIOSIGNALPROCESSING\_モード**の基本サポートハンドラーは、 **KSP\_PIN**構造体に渡す必要があります。また、非ループバックストリーミングピンでのみサポートを提供する必要があります。 オーディオドライバーは、ホストとオフロードの pin でのみシグナル処理モードをサポートする必要があります。 ループバックまたはブリッジの pin では、オーディオドライバーは引き続きプロパティをサポートする必要がありますが、 *Count*パラメーターを 0 (0) に設定して、 **KSMULTIPLE\_ITEM**構造体を返します。

Microsoft オーディオポートクラスドライバー (Portcls) で動作するように開発されたオーディオミニポートドライバーは、 [**IMiniportAudioSignalProcessing:: GetModes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportaudiosignalprocessing-getmodes)メソッドを実装できます。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows 8.1</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**IMiniportAudioSignalProcessing:: GetModes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportaudiosignalprocessing-getmodes)

[KSMULTIPLE\_項目](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)

[KSP\_ピン留め](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)

 

 






