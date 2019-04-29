---
title: KSPROPERTY\_AUDIOSIGNALPROCESSING\_モード
description: KSPROPERTY\_AUDIOSIGNALPROCESSING\_モード プロパティは、pin factory でサポートされるオーディオ信号処理モードの一覧を返します。
ms.assetid: 95536F80-D4E0-48CB-8DB2-603C4CEF0053
keywords:
- KSPROPERTY_AUDIOSIGNALPROCESSING_MODES オーディオ デバイス
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
ms.openlocfilehash: 378c8d57eca8631826af6edb56be9af0797c3105
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332792"
---
# <a name="kspropertyaudiosignalprocessingmodes"></a>KSPROPERTY\_AUDIOSIGNALPROCESSING\_モード


**KSPROPERTY\_AUDIOSIGNALPROCESSING\_モード**pin factory でサポートされるオーディオ信号処理モードの一覧を返します。

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
<td align="left"><p>(フィルター インスタンス) を使用してファクトリをピン留めします。</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566722.aspx" data-raw-source="[KSP_PIN](https://msdn.microsoft.com/library/windows/hardware/ff566722.aspx)">KSP_PIN</a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff563441.aspx" data-raw-source="[KSMULTIPLE_ITEM](https://msdn.microsoft.com/library/windows/hardware/ff563441.aspx)">KSMULTIPLE_ITEM</a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値は、構造、後にゼロ (0) または複数の Guid です。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

**KSPROPERTY\_AUDIOSIGNALPROCESSING\_モード**を返します、 **KSMULTIPLE\_項目**の後にゼロ (0) または複数の GUID。 KSMULTIPLE\_項目。Count メンバーには、Guid の番号が含まれています。 KSMULTIPLE\_項目。サイズのメンバーには、プロパティ値の合計サイズが含まれています。 指定した暗証番号 (pin) の ID のオーディオ ドライバーでサポートされるシグナル処理モードを識別する GUID ごと、 *PinId*のメンバー、 **KSP\_PIN**構造体。

Windows 8.1 では、定義されているオーディオ信号処理の 2 つのモード、オーディオが\_SIGNALPROCESSINGMODE\_既定とオーディオ\_SIGNALPROCESSINGMODE\_RAW です。

Windows 10 では、追加の 5 つのモードが定義されます。

オーディオ\_SIGNALPROCESSINGMODE\_通信オーディオ\_SIGNALPROCESSINGMODE\_音声オーディオ\_SIGNALPROCESSINGMODE\_MEDIA オーディオ\_SIGNALPROCESSINGMODE\_ムービー オーディオ\_SIGNALPROCESSINGMODE\_詳細については、通知を参照してください[オーディオ信号の処理モード](https://msdn.microsoft.com/windows/hardware/drivers/audio/audio-signal-processing-modes)します。

<a name="remarks"></a>注釈
-------

基本的なサポート ハンドラー **KSPROPERTY\_AUDIOSIGNALPROCESSING\_モード**渡される必要があります、 **KSP\_PIN**構造体、およびサポートのみを提供する必要がありますループバック以外では、ピンをストリーミングします。 オーディオ ドライバーは、ホスト上のみシグナル処理モードをサポートし、ピンの負荷を軽減する必要があります。 ループバックまたはブリッジのピンのオーディオ ドライバーもプロパティをサポートしてを返す、 **KSMULTIPLE\_項目**構造体の*カウント*パラメーターがゼロ (0) に設定します。

オーディオ ポート クラス ドライバー (Portcls) を実装できる Microsoft と協力する開発したオーディオ ミニポート ドライバー、 [ **IMiniportAudioSignalProcessing::GetModes** ](https://msdn.microsoft.com/library/windows/hardware/dn457660)メソッド。

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

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**IMiniportAudioSignalProcessing::GetModes**](https://msdn.microsoft.com/library/windows/hardware/dn457660)

[KSMULTIPLE\_項目](https://msdn.microsoft.com/library/windows/hardware/ff563441.aspx)

[KSP\_暗証番号 (PIN)](https://msdn.microsoft.com/library/windows/hardware/ff566722.aspx)

 

 






