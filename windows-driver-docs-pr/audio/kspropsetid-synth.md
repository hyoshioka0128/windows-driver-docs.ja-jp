---
title: KSPROPSETID\_シンセサイザー
description: KSPROPSETID\_シンセサイザー
ms.assetid: ff5efd85-0b4d-4625-b029-fecf325bcacb
keywords:
- KSPROPSETID_Synth
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e18d48653f747c8b77ac4ee23146532031b94b87
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830459"
---
# <a name="kspropsetid_synth"></a>KSPROPSETID\_シンセサイザー


## <span id="ddk_kspropsetid_synth_ks"></span><span id="DDK_KSPROPSETID_SYNTH_KS"></span>


`KSPROPSETID_Synth` プロパティセットには、シンセサイザーノード ([**KSNODETYPE\_シンセサイザー**](ksnodetype-synthesizer.md)) の構成に対してグローバルなプロパティが含まれています。

このセットのプロパティ項目は、ヘッダーファイル Dマス Prop. h で定義されているように、KSK プロパティ\_シンセサイザー列挙値によって指定されます。

## <span id="ddk_ksproperty_synth_caps_ks"></span><span id="DDK_KSPROPERTY_SYNTH_CAPS_KS"></span>


### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

KSK プロパティ\_シンセサイザー\_CAPS プロパティは、シンセサイザーの機能を決定するためにシステムによって使用されます。

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
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusprop/ns-dmusprop-_synthcaps" data-raw-source="[&lt;strong&gt;SYNTHCAPS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusprop/ns-dmusprop-_synthcaps)"><strong>SYNTHCAPS</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、SYNTHCAPS 型の構造であり、シンセサイザーの機能を指定します。 次のような機能があります。

-   使用可能なサンプルメモリの量

-   チャネルグループの最大数

-   音声の最大数

-   オーディオチャンネルの最大数

-   レンダリング効果

詳細については、「 [**Synthcaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusprop/ns-dmusprop-_synthcaps)」を参照してください。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

の KSK プロパティ\_シンセサイザー\_CAPS プロパティ要求は正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

シンセサイザーの機能の詳細については、Microsoft Windows SDK のドキュメントの「 **IDirectMusicPort:: getcaps**メソッド」と「dmus\_portcaps 構造体」を参照してください。

## <span id="ddk_ksproperty_synth_channelgroups_ks"></span><span id="DDK_KSPROPERTY_SYNTH_CHANNELGROUPS_KS"></span>


### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

KSK プロパティ\_シンセサイザー\_CHANNELGROUPS プロパティは、pin インスタンス上のアクティブなチャネルグループの数を設定または取得するためにシステムによって使用されます。 チャネルグループは、各 pin インスタンスに対して0から始まる番号が付けられます。

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
<td align="left"><p>[はい]</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は ULONG 型で、pin がサポートするチャネルグループの数を指定します。 Pin で*n*チャネルグループがサポートされている場合、pin のチャネルグループには 0 ~ *n*-1 の番号が付けられます。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

の KSK プロパティ\_シンセサイザー\_CAPS プロパティ要求は正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。 次の表に、考えられるエラーコードを示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">状態コード</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>STATUS_BUFFER_TOO_SMALL</p></td>
<td align="left"><p>バッファーが小さすぎて操作を完了できませんでした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_UNSUCCESSFUL</p></td>
<td align="left"><p>操作は正常に完了しませんでした。</p></td>
</tr>
</tbody>
</table>

 

チャネルグループの詳細については、Microsoft Windows SDK のドキュメントの**IDirectMusicPort:: getnumchannelgroups**メソッドと**IDirectMusicPort:: setnumchannelgroups**メソッドの説明を参照してください。

## <span id="ddk_ksproperty_synth_latencyclock_ks"></span><span id="DDK_KSPROPERTY_SYNTH_LATENCYCLOCK_KS"></span>


### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

KSK プロパティ\_シンセサイザー\_LATENCYCLOCK プロパティは、ストリームの現在の待機時間の時刻をミニポートドライバーに照会するために使用されます。これは、常にマスタークロック時間よりも大きくなります。

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
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>ULONGLONG</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は ULONGLONG 型で、シンセサイザーの現在の待機時間を表します。 この時刻は、マスタークロックに対して相対的に指定され、100ナノ秒単位で表されます。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_シンセサイザー\_LATENCYCLOCK property 要求は、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。 次の表に、考えられるエラーコードを示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">状態コード</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>STATUS_BUFFER_TOO_SMALL</p></td>
<td align="left"><p>バッファーが小さすぎて操作を完了できませんでした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_UNSUCCESSFUL</p></td>
<td align="left"><p>操作は正常に完了しませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_INVALID_DEVICE_REQUEST</p></td>
<td align="left"><p>このデバイスでは、この操作は無効です。</p></td>
</tr>
</tbody>
</table>

 

待機時間クロックは、通常、オーディオ出力ストリームを複数のデバイス間で同期するために使用されます。

KSK プロパティ\_シンセサイザー\_LATENCYCLOCK 要求では、現在のマスタークロック時間と同じ待機時間 (クロック時間) と、ストリームが通過するオーディオフィルターの最小待機時間を返す必要があります。 現在の待機時間の時間が経過したときに再生されるオーディオデータをスケジュールするアプリケーションプログラム。データが遅れて再生されるリスクがあります。

待機時間の詳細については、次を参照してください。

-   [待機時間クロック](https://docs.microsoft.com/windows-hardware/drivers/audio/latency-clocks)での ksk プロパティ\_シンセサイザー\_LATENCYCLOCK プロパティについて説明します。

-   Microsoft Windows SDK ドキュメントの**IDirectMusicPort:: GetLatencyClock**メソッドと**Ireferenceclock:: GetTime**メソッドの説明。

## <span id="ddk_ksproperty_synth_portparameters_ks"></span><span id="DDK_KSPROPERTY_SYNTH_PORTPARAMETERS_KS"></span>


### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

"KSK プロパティ\_シンセサイザー\_PORTPARAMETERS" プロパティは、DirectMusic*ポート*の構成パラメーターを取得するために使用されます。これは、音楽データを送信または受信するデバイスの directmusic 用語です。 (KS の用語では、DirectMusic ポートは DMus ポートドライバーに対応していません。 これは、DirectMusic フィルターのレンダーピンまたは capture ピンに対応します)。

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
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a> + <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusprop/ns-dmusprop-_synth_portparams" data-raw-source="[&lt;strong&gt;SYNTH_PORTPARAMS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusprop/ns-dmusprop-_synth_portparams)"> <strong>SYNTH_PORTPARAMS</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusprop/ns-dmusprop-_synth_portparams" data-raw-source="[&lt;strong&gt;SYNTH_PORTPARAMS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusprop/ns-dmusprop-_synth_portparams)"><strong>SYNTH_PORTPARAMS</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ記述子 (インスタンスデータ) は、KSNODEPROPERTY 構造体で構成され、その直後には、その直後に、データの\_PORTPARAMS 構造体が続きます。 クライアントは、プロパティ要求を送信する前に、要求されたパラメーター値を、シンセ\_PORTPARAMS 構造体に書き込むことによって指定します。

プロパティ値 (操作データ) の種類は、\_PORTPARAMS でもあります。 ミニポートドライバーは、ポートの構成に実際に使用するパラメーター値を使用して、この構造体を読み込みます。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

ミニポートドライバーが、呼び出し元によって指定されたとおりに DirectMusic ポートの構成に成功した場合は、状態\_成功コードとして返されます。 それ以外の場合は、適切なエラーコードを返します。 次の表は、考えられるエラー状態コードの一部を示しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">状態コード</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>STATUS_NOT_ALL_ASSIGNED</p></td>
<td align="left"><p>操作は成功しましたが、ミニポートドライバーは、呼び出し元がプロパティ値で有効としてマークした1つ以上のパラメーター値を変更する必要がありました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_UNSUCCESSFUL</p></td>
<td align="left"><p>操作は正常に完了しませんでした。</p></td>
</tr>
</tbody>
</table>

 

これは、処理する DirectMusic プロパティ項目の中で最も複雑なものです。 このプロパティでは get 要求のみがサポートされますが、get 要求ではポートパラメーターも設定されます。 ポートは、プロパティ要求のプロパティ記述子として、\_PORTPARAMS 構造体を渡します。 プロパティ値バッファーはプロパティ要求に付随していますが、これは get 要求であるため、バッファーはミニポートドライバーから情報を取得するためだけに使用されます。

ミニポートドライバーは、最初に、プロパティ記述子からプロパティ値バッファーに、シンセ\_PORTPARAMS 構造体をコピーする必要があります。 次に、呼び出し元が要求したすべてのパラメーター値 (有効としてマークされている) をサポートできるかどうかを確認する必要があります。 1つまたは複数の要求されたパラメーター値をミニポートドライバーがサポートできない場合は、その特定のパラメーターに対して指定された値を使用して、指定したパラメーターの値を\_上書きする必要があります。ご.

ミニポートドライバーによって、呼び出し元のシンセサイザー\_PORTPARAMS に変更が加えられない場合、呼び出し元は、呼び出し元が最初にミニポートドライバーに送信したプロパティ記述子のパラメーターと正確に一致するプロパティ値を返す必要があります。

規則により、ドライバーは、シンセサイザー\_PORTPARAMS の**Dwvalidparams**メンバーに対応するビットが設定されていないパラメーターの値も入力します。 これにより、呼び出し元は、これらのパラメーターに対してミニポートドライバーが使用する既定値を確認できます。 ミニポートドライバーは、wave インターフェイスデバイスを構築するために使用した実際のパラメーター値を出力します。

サンプルレートの変更に対する要求を正しく処理するには、ミニポートドライバーの KSK プロパティ\_シンセサイザー\_PORTPARAMETERS ハンドラーを準備する必要があります。

## <span id="ddk_ksproperty_synth_runningstats_ks"></span><span id="DDK_KSPROPERTY_SYNTH_RUNNINGSTATS_KS"></span>


### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

KSK プロパティ\_シンセサイザー\_RUNNINGSTATS プロパティは、シンセサイザーのパフォーマンス統計情報をミニポートドライバーに照会するために使用されます。

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
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusprop/ns-dmusprop-_synth_stats" data-raw-source="[&lt;strong&gt;SYNTH_STATS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusprop/ns-dmusprop-_synth_stats)"><strong>SYNTH_STATS</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、\_STATS 型の構造体です。 ミニポートドライバーのプロパティハンドラーは、次の統計情報をこの構造体に書き込みます。

-   再生の平均数

-   CPU 使用率

-   失われたメモの数

-   空きメモリ容量

-   ピーク時のボリュームレベル

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_シンセサイザー\_RUNNINGSTATS property 要求は、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。 次の表に、考えられるエラーコードを示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">状態コード</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>STATUS_BUFFER_TOO_SMALL</p></td>
<td align="left"><p>バッファーが小さすぎて操作を完了できませんでした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_UNSUCCESSFUL</p></td>
<td align="left"><p>操作は正常に完了しませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_INVALID_DEVICE_REQUEST</p></td>
<td align="left"><p>このデバイスでは、この操作は無効です。</p></td>
</tr>
</tbody>
</table>

 

デバイスが KSK 状態\_実行状態のままになっている間、シンセサイザーのパフォーマンス統計が継続的に更新されます。 デバイスがこの状態になるたびに、統計がリセットされます。これにより、ピークボリュームや失われたメモの数などの累積値がゼロになります。

詳細については、Microsoft Windows SDK のドキュメントで、 **IDirectMusicPort:: GetRunningStats**メソッドと dmus\_SYNTHSTATS 構造体の説明を参照してください。

## <span id="ddk_ksproperty_synth_voicepriority_ks"></span><span id="DDK_KSPROPERTY_SYNTH_VOICEPRIORITY_KS"></span>


### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

KSK プロパティ\_シンセサイザー\_VOICEPRIORITY プロパティは、ミニポートドライバーが音声キャッシュから音声を取得する必要がある場合に、MIDI シンセサイザー内の特定の音声が持つ優先度を指定します。

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
<td align="left"><p>[はい]</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a> + <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusprop/ns-dmusprop-_synthvoicepriority_instance" data-raw-source="[&lt;strong&gt;SYNTHVOICEPRIORITY_INSTANCE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusprop/ns-dmusprop-_synthvoicepriority_instance)"> <strong>SYNTHVOICEPRIORITY_INSTANCE</strong></a></p></td>
<td align="left"><p>DWORD</p></td>
</tr>
</tbody>
</table>

 

プロパティ記述子 (インスタンスデータ) は、KSNODEPROPERTY 構造体で構成されます。この構造体には、直後に SYNTHVOICEPRIORITY\_インスタンス構造が続きます。この構造では、音声のチャネルグループ (16 の MIDI チャネルのセット) とチャネル番号 (グループ)。

プロパティ値 (操作データ) は、優先度を指定する DWORD です。 クライアントは、KSK プロパティ\_シンセサイザー\_VOICEPRIORITY 要求を使用して、ボイスの新しい優先順位をミニポートドライバーに送信します。また、KSK プロパティ\_シンセサイザー\_VOICEPRIORITY の get プロパティ要求を使用して音声を取得します。ミニポートドライバーからの現在の優先順位。

**音声の優先度**

次のチャネルグループの優先順位は、ヘッダーファイル Dマス Prop. h で定義されています。

```cpp
  DAUD_CRITICAL_VOICE_PRIORITY
  DAUD_HIGH_VOICE_PRIORITY
  DAUD_STANDARD_VOICE_PRIORITY
  DAUD_LOW_VOICE_PRIORITY
  DAUD_PERSIST_VOICE_PRIORITY
```

上記のリストは、最上位の優先順位と一番下の方の順に並んでいます。 これらの優先順位は、チャネルグループ内の各チャネルの音声優先順位に到達するチャネル優先順位オフセットと共に使用されます。 結果として得られる優先順位は、get および set プロパティの要求で渡されます。

上記のチャネルグループの優先順位値は、チャネルの優先順位オフセットと比較して大きくなります。 その結果、チャネルグループの優先順位を変更すると、チャネルグループ内のチャネルの相対的な優先順位を変更せずに、他のチャネルグループを基準にして、チャネルグループ全体の優先順位を上げたり下げたりすることになります。

### <a name="span-iddefault_prioritiesspanspan-iddefault_prioritiesspan-default-priorities"></a><span id="default_priorities"></span><span id="DEFAULT_PRIORITIES"></span>既定の優先順位

シンセサイザーミニポートドライバーが作成されると、各音声に既定の優先順位が割り当てられます。 既定値は次のように定義されています。

-   既定では、優先順位はチャネルグループによって異なります。 これは、たとえば、チャネルグループ1のチャネル5は、チャネルグループ2のチャネル5と同じ優先順位を持つことを意味します。

-   DLS レベル1の仕様に従って、チャネル 10 (MIDI percussion チャネル) の優先順位は最も高くなり、その後に 1 ~ 9 および 11 ~ 16 が続きます。

ヘッダーファイル Dマス Prop は、次の優先順位のオフセットを定義します。

```cpp
  DAUD_CHAN10_VOICE_PRIORITY_OFFSET
  DAUD_CHAN1_VOICE_PRIORITY_OFFSET
  DAUD_CHAN2_VOICE_PRIORITY_OFFSET
  DAUD_CHAN3_VOICE_PRIORITY_OFFSET
  DAUD_CHAN4_VOICE_PRIORITY_OFFSET
  DAUD_CHAN5_VOICE_PRIORITY_OFFSET
  DAUD_CHAN6_VOICE_PRIORITY_OFFSET
  DAUD_CHAN7_VOICE_PRIORITY_OFFSET
  DAUD_CHAN8_VOICE_PRIORITY_OFFSET
  DAUD_CHAN9_VOICE_PRIORITY_OFFSET
  DAUD_CHAN11_VOICE_PRIORITY_OFFSET
  DAUD_CHAN12_VOICE_PRIORITY_OFFSET
  DAUD_CHAN13_VOICE_PRIORITY_OFFSET
  DAUD_CHAN14_VOICE_PRIORITY_OFFSET
  DAUD_CHAN15_VOICE_PRIORITY_OFFSET
  DAUD_CHAN16_VOICE_PRIORITY_OFFSET
```

上記のオフセットの一覧は、優先順位が最も高い順に一覧の一番上に表示されます。 また、ヘッダーファイル Dマスを使用すると、各チャネルグループ内のチャネルの既定の優先順位も定義されます。これにより、これらの各オフセットが DAUD\_標準\_音声\_優先順位になります。 たとえば、次の定義は、各チャネルグループのチャネル1の既定の優先順位を示しています。

```cpp
  #define DAUD_CHAN1_DEF_VOICE_PRIORITY \
    (DAUD_STANDARD_VOICE_PRIORITY | DAUD_CHAN1_VOICE_PRIORITY_OFFSET)
```

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_シンセサイザー\_VOICEPRIORITY property 要求は、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。 次の表に、考えられるエラーコードを示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">状態コード</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>STATUS_BUFFER_TOO_SMALL</p></td>
<td align="left"><p>バッファーが小さすぎて操作を完了できませんでした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_UNSUCCESSFUL</p></td>
<td align="left"><p>操作は正常に完了しませんでした。</p></td>
</tr>
</tbody>
</table>

 

音声の優先順位の詳細については、Microsoft Windows SDK のドキュメントで**IDirectMusicPort:: getchannelpriority**メソッドと**IDirectMusicPort:: setchannelpriority**メソッドの説明を参照してください。

## <span id="ddk_ksproperty_synth_volume_ks"></span><span id="DDK_KSPROPERTY_SYNTH_VOLUME_KS"></span>


### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

KSK プロパティ\_シンセサイザー\_VOLUME プロパティは、シンセサイザーデバイスのボリュームレベルを取得または設定します。

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
<td align="left"><p>[はい]</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p>長い</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は LONG 型で、シンセサイザーデバイスのボリュームレベルを指定します。 ボリュームの設定は、1/100 単位で指定します。 ミニポートドライバーは、プロパティを取得するか設定するかに応じて、ボリュームを変更するか、ボリュームを報告する必要があります。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_シンセサイザー\_ボリュームプロパティ要求は、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。 次の表に、考えられるエラーコードを示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">状態コード</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>STATUS_BUFFER_TOO_SMALL</p></td>
<td align="left"><p>バッファーが小さすぎて操作を完了できませんでした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_UNSUCCESSFUL</p></td>
<td align="left"><p>操作は正常に完了しませんでした。</p></td>
</tr>
</tbody>
</table>

 

## <span id="ddk_ksproperty_synth_volumeboost_ks"></span><span id="DDK_KSPROPERTY_SYNTH_VOLUMEBOOST_KS"></span>


### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

KSK プロパティ\_シンセサイザー\_VOLUMEBOOST ストプロパティは、シンセサイザーデバイスのボリュームをブーストする量を指定します。

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
<td align="left"><p>[はい]</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>長い</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は LONG 型で、ミックスステージの後にオーディオ信号をブーストする量によって指定されます。 これは、すべての音声 articulation とミックスが完了した後に、シンセサイザーの最終出力に追加するボリュームの量です。 ボリュームブースト量は、1/100 単位で指定されます。 この値には、正または負の値を指定できます。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_シンセサイザー\_VOLUMEBOOST ストプロパティ要求は、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。 次の表に、考えられるエラーコードを示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">状態コード</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>STATUS_BUFFER_TOO_SMALL</p></td>
<td align="left"><p>バッファーが小さすぎて操作を完了できませんでした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_UNSUCCESSFUL</p></td>
<td align="left"><p>操作は正常に完了しませんでした。</p></td>
</tr>
</tbody>
</table>

 

他のブーストを出力に追加することはできません。 シンセサイザーは、articulation の厳密な DLS レベル1規則に従う必要があります。

このプロパティは、シンセサイザーの音量をシステム内の他のオーディオ出力とイコライズするために使用されます。したがって、増加量はすべてのデバイスで一貫した方法で解釈されます。

 

 





