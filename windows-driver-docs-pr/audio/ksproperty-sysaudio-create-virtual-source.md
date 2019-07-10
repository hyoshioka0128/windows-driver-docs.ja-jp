---
title: KSPROPERTY\_SYSAUDIO\_作成\_仮想\_ソース
description: KSPROPERTY\_SYSAUDIO\_作成\_仮想\_ソース プロパティは、新しい仮想ソースを作成します。
ms.assetid: 771c4084-8007-4280-8451-946a26182740
keywords:
- KSPROPERTY_SYSAUDIO_CREATE_VIRTUAL_SOURCE オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_SYSAUDIO_CREATE_VIRTUAL_SOURCE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a311819918c751758b70694759d140e3ea2e98b
ms.sourcegitcommit: fee68bc5f92292281ecf1ee88155de45dfd841f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716816"
---
# <a name="kspropertysysaudiocreatevirtualsource"></a>KSPROPERTY\_SYSAUDIO\_作成\_仮想\_ソース


KSPROPERTY\_SYSAUDIO\_作成\_仮想\_ソース プロパティは、新しい仮想ソースを作成します。

## <span id="ddk_ksproperty_sysaudio_create_virtual_source_ks"></span><span id="DDK_KSPROPERTY_SYSAUDIO_CREATE_VIRTUAL_SOURCE_KS"></span>


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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-sysaudio_create_virtual_source" data-raw-source="[&lt;strong&gt;SYSAUDIO_CREATE_VIRTUAL_SOURCE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-sysaudio_create_virtual_source)"><strong>SYSAUDIO_CREATE_VIRTUAL_SOURCE</strong></a></p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティ記述子 (インスタンス データ) は、型 SYSAUDIO の構造\_作成\_仮想\_仮想のソースのピン留めするカテゴリと暗証番号 (pin) 名の Guid を指定するソース。

プロパティの値 (データの操作) は、仮想のソースのインデックスを含む ULONG 変数です。 SysAudio では、新しい仮想ソースを識別するには、このインデックスを生成します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_SYSAUDIO\_作成\_仮想\_ソース プロパティの要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

このプロパティは、ボリュームなど仮想ミキサー行ソースを作成またはコントロールをミュートに使用されます。

SysAudio が同じ pin カテゴリおよび pin 名前 Guid と、KSPROPERTY 仮想ソースを作成して既に場合\_SYSAUDIO\_作成\_仮想\_ソース プロパティの get 要求は、既存のインデックスを取得します。仮想のソース。 それ以外の場合、要求は、新しい仮想ソース インデックスを生成し、その値を出力します。

SysAudio が仮想のソースにインデックスを割り当てられた後、 [ **KSPROPERTY\_SYSAUDIO\_アタッチ\_仮想\_ソース**](ksproperty-sysaudio-attach-virtual-source.md)プロパティの設定その仮想のソースを仮想のオーディオ デバイスの暗証番号 (pin) のインスタンスにアタッチする要求を使用できます。

ユーザーは、SndVol32 アプリケーションを通じてさまざまなオーディオ ソースのボリューム レベルを制御します。 これらのソースには、wave 出力デバイス、MIDI シンセサイザー、CD プレーヤー、およびライン入力ジャックが含まれます。 SndVol32 Windows マルチ メディアを使用して**waveOut**_Xxx_、 **midiOut**_Xxx_、および**aux** _Xxx_これらのソース ボリューム レベルを制御する関数。 Windows のマルチ メディア機能の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

SysAudio では、これらのデバイスにボリュームの変更をインターセプトし、その仮想ソースに適用します。 たとえば、MIDI ファイルを wave データに変換するソフトウェア MIDI シンセサイザーが仮想のオーディオ デバイス wave レンダリング ピンのいずれかに接続されている場合、SysAudio は適用 midiOut*Xxx*ボリュームは、pin を変更 (ではなく**waveOut**_Xxx_ボリュームの変更)。 同様に場合、 [Redbook システム ドライバー](https://docs.microsoft.com/windows-hardware/drivers/audio/kernel-mode-wdm-audio-components#redbook-system-driver)、CD プレーヤーからデジタル音楽、波形データを変換が仮想のオーディオ デバイス wave レンダリング ピンのいずれかに接続されている、SysAudio 適用 AUXCAPS\_オーディオのボリュームpin を変更します。 詳細については、AUXCAPS\_オーディオ構造体を Windows SDK のマニュアルを参照してください。

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


[**SYSAUDIO\_作成\_仮想\_ソース**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-sysaudio_create_virtual_source)

[**KSPROPERTY\_SYSAUDIO\_アタッチ\_仮想\_ソース**](ksproperty-sysaudio-attach-virtual-source.md)

 

 






