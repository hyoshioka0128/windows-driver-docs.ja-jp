---
title: KSPROPERTY\_オーディオ\_DEV\_特定
description: KSPROPERTY\_オーディオ\_DEV\_デバイスに固有のノードでデバイスに固有のプロパティにアクセスする特定のプロパティが使用される (KSNODETYPE\_DEV\_特定) します。
ms.assetid: f3f2e340-7403-4c86-841f-7008afda28a5
keywords:
- KSPROPERTY_AUDIO_DEV_SPECIFIC オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_DEV_SPECIFIC
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd1b56d5f89cf793677082e9197c3da2718d73e7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333061"
---
# <a name="ksproperty_audio_dev_specific"></a>KSPROPERTY\_オーディオ\_DEV\_特定


`KSPROPERTY_AUDIO_DEV_SPECIFIC`デバイスに固有のノードでデバイスに固有のプロパティにアクセスするプロパティを使用 ([**KSNODETYPE\_DEV\_特定**](ksnodetype-dev-specific.md))。

## <span id="ddk_ksproperty_audio_dev_specific_ks"></span><span id="DDK_KSPROPERTY_AUDIO_DEV_SPECIFIC_KS"></span>


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
<th align="left">取得</th>
<th align="left">設定</th>
<th align="left">対象</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>&lt;デバイスに固有&gt;</p></td>
<td align="left"><p>&lt;デバイスに固有&gt;</p></td>
<td align="left"><p>&lt;デバイスに固有&gt;</p></td>
<td align="left"><p>&lt;デバイスに固有&gt;</p></td>
<td align="left"><p>&lt;デバイスに固有&gt;</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、デバイス固有の書式で表されます。

プロパティが get または set プロパティの要求をサポートしているかどうかが特定のデバイスもです。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

このプロパティは、いずれかの状態を返します\_成功またはオーディオ ドライバーのサード パーティ プロバイダーによって決定されるデバイスの特定値。

<a name="remarks"></a>注釈
-------

Windows Vista および Windows では、追加のタブの以降のバージョン (というラベルの付いた**カスタム**) で提供される、**サウンド**アプレット**コントロール パネルの** 。 **カスタム** タブには、自動ゲイン制御 (AGC) およびデバイス固有のプロパティのコントロールが表示されます。 次の表は、コントロールで公開されている、**サウンド**、各種のアプレット`KSPROPERTY_AUDIO_DEV_SPECIFIC`プロパティとデータ型の組み合わせ。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">KSPROPERTY</th>
<th align="left">データの種類</th>
<th align="left">コントロール</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="ksproperty-audio-agc.md" data-raw-source="[&lt;strong&gt;KSPROPERTY_AUDIO_AGC&lt;/strong&gt;](ksproperty-audio-agc.md)"><strong>KSPROPERTY_AUDIO_AGC</strong></a></p></td>
<td align="left"><p>BOOL</p></td>
<td align="left"><p>チェック ボックス</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSPROPERTY_AUDIO_DEV_SPECIFIC</p></td>
<td align="left"><p>BOOL</p></td>
<td align="left"><p>チェック ボックス</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSPROPERTY_AUDIO_DEV_SPECIFIC</p></td>
<td align="left"><p>LONG</p></td>
<td align="left"><p>スライダー</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSPROPERTY_AUDIO_DEV_SPECIFIC</p></td>
<td align="left"><p>ULONG</p></td>
<td align="left"><p>スライダー</p></td>
</tr>
</tbody>
</table>

 

**KSPROPERTY\_オーディオ\_AGC**デバイスでの実際の AGC 機能を公開するために使用する必要があります。 その他のデバイス固有の機能を使用して公開する必要があります`KSPROPERTY_AUDIO_DEV_SPECIFIC`します。

参照してください、**カスタム** タブで、オーディオのレンダリングまたはでキャプチャ デバイスを選択、**サウンド**アプレットとクリック*プロパティ*します。

プロパティのハンドラーを実装する方法の例については、`KSPROPERTY_AUDIO_DEV_SPECIFIC`プロパティを参照してください、 **CMiniportTopologyMSVAD::PropertyHandlerDevSpecific** Basetopo.cpp ファイル内のメソッド。

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
<td align="left"><p>Windows Vista および Windows オペレーティング システムの以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>参照してください。


[**KSNODETYPE\_DEV\_特定**](ksnodetype-dev-specific.md)

[**KSPROPERTY\_オーディオ\_AGC**](ksproperty-audio-agc.md)

 

 






