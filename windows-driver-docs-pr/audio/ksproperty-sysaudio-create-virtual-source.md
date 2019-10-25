---
title: KSK プロパティ\_SYSAUDIO\_作成\_仮想\_ソース
description: KSK プロパティ\_SYSAUDIO\_CREATE\_VIRTUAL\_SOURCE プロパティは、新しい仮想ソースを作成します。
ms.assetid: 771c4084-8007-4280-8451-946a26182740
keywords:
- KSPROPERTY_SYSAUDIO_CREATE_VIRTUAL_SOURCE オーディオデバイス
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
ms.openlocfilehash: 272c9f1d3ca5f97e090a7576f44b71b90539c2cf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832730"
---
# <a name="ksproperty_sysaudio_create_virtual_source"></a>KSK プロパティ\_SYSAUDIO\_作成\_仮想\_ソース


KSK プロパティ\_SYSAUDIO\_CREATE\_VIRTUAL\_SOURCE プロパティは、新しい仮想ソースを作成します。

## <span id="ddk_ksproperty_sysaudio_create_virtual_source_ks"></span><span id="DDK_KSPROPERTY_SYSAUDIO_CREATE_VIRTUAL_SOURCE_KS"></span>


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
<td align="left"><p>フィルター</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sysaudio_create_virtual_source" data-raw-source="[&lt;strong&gt;SYSAUDIO_CREATE_VIRTUAL_SOURCE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sysaudio_create_virtual_source)"><strong>SYSAUDIO_CREATE_VIRTUAL_SOURCE</strong></a></p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティ記述子 (インスタンスデータ) は SYSAUDIO 型の構造であり、仮想ソースのピンカテゴリと pin 名の Guid を指定する\_仮想\_ソースを作成\_ます。

プロパティ値 (操作データ) は、仮想ソースインデックスを含む ULONG 変数です。 SysAudio は、このインデックスを生成して新しい仮想ソースを識別します。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_SYSAUDIO\_作成\_仮想\_ソースプロパティ要求は、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

このプロパティは、ボリュームやミュートのコントロールなど、ミキサーラインの仮想ソースを作成するために使用されます。

SysAudio によって既に同じピンカテゴリと pin 名の Guid を持つ仮想ソースが作成されている場合は、KSK プロパティ\_SYSAUDIO\_作成\_仮想\_ソースのプロパティの要求では、既存の仮想ソースのインデックスを取得します。 それ以外の場合は、要求によって新しい仮想ソースインデックスが生成され、その値が出力されます。

SysAudio によって仮想ソースにインデックスが割り当てられた後は、 [**Ksk プロパティ\_sysaudio\_アタッチ\_仮想\_ソース**](ksproperty-sysaudio-attach-virtual-source.md)セットのプロパティの要求を使用して、仮想オーディオデバイス上のピンインスタンスに仮想ソースをアタッチできます。

ユーザーは、SndVol32 アプリケーションを使用して、さまざまなオーディオソースのボリュームレベルを制御します。 これらのソースには、wave 出力デバイス、MIDI シンセサイザー、CD プレーヤー、およびライン入力ジャックが含まれます。 SndVol32 は、Windows マルチメディア**waveOut**_xxx_、 **midiout**_xxx_、および**aux**_xxx_の各関数を使用して、これらのソースのボリュームレベルを制御します。 Windows マルチメディア機能の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

SysAudio は、これらのデバイスに対して行われたボリュームの変更をインターセプトし、仮想ソースに適用します。 たとえば、MIDI ファイルを wave データに変換するソフトウェア MIDI シンセサイザーが、仮想オーディオデバイスの wave レンダリングピンのいずれかに接続されている場合、SysAudio は**waveOut**_xxx_の代わりに、midiout*Xxx*ボリュームの変更をピンに適用します。ボリュームの変更)。 同様に、デジタルオーディオを CD プレーヤーから wave データに変換する[Redbook システムドライバー](https://docs.microsoft.com/windows-hardware/drivers/audio/kernel-mode-wdm-audio-components#redbook-system-driver)が仮想オーディオデバイスの wave レンダリングピンのいずれかに接続されている場合、SYSAUDIO は AUXCAPS\_cdaudio ボリュームの変更を pin に適用します。 AUXCAPS\_CDAUDIO 構造体の詳細については、Windows SDK のドキュメントを参照してください。

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


[**SYSAUDIO\_\_仮想\_ソースの作成**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sysaudio_create_virtual_source)

[**KSK プロパティ\_SYSAUDIO\_接続\_仮想\_ソース**](ksproperty-sysaudio-attach-virtual-source.md)

 

 






