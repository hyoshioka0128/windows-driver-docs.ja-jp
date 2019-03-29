---
title: KSPROPSETID\_シンセサイザー
description: KSPROPSETID\_シンセサイザー
ms.assetid: ff5efd85-0b4d-4625-b029-fecf325bcacb
keywords:
- KSPROPSETID_Synth
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8bd1f6d5109c080fbc486ca838213a1890948d40
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572940"
---
# <a name="kspropsetidsynth"></a>KSPROPSETID\_シンセサイザー


## <span id="ddk_kspropsetid_synth_ks"></span><span id="DDK_KSPROPSETID_SYNTH_KS"></span>


`KSPROPSETID_Synth`シンセサイザー ノードの構成のグローバルなプロパティがプロパティ セットに含まれています ([**KSNODETYPE\_シンセサイザー**](ksnodetype-synthesizer.md))。

このセット内のプロパティ項目が KSPROPERTY によって指定された\_シンセサイザー列挙値では、ヘッダーで定義されているファイル Dmusprop.h します。

## <span id="ddk_ksproperty_synth_caps_ks"></span><span id="DDK_KSPROPERTY_SYNTH_CAPS_KS"></span>


### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

KSPROPERTY\_シンセサイザー\_CAPS プロパティは、シンセサイザーの機能を決定する、システムによって使用されます。

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
<th align="left">Set</th>
<th align="left">移行先</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>はい</p></td>
<td align="left"><p>いいえ</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537143" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537143)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff538424" data-raw-source="[&lt;strong&gt;SYNTHCAPS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff538424)"><strong>SYNTHCAPS</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) では、型 SYNTHCAPS の構造体をシンセサイザーの機能を指定します。 これらの機能は次のとおりです。

-   使用可能なサンプルのメモリの量

-   チャネルのグループの最大数

-   音声の最大数

-   オーディオ チャネルの最大数

-   効果のレンダリング

詳細については、次を参照してください。 [ **SYNTHCAPS**](https://msdn.microsoft.com/library/windows/hardware/ff538424)します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_シンセサイザー\_CAPS プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

シンセサイザーの機能の詳細については、次を参照してください。、 **IDirectMusicPort::GetCaps**メソッドと、DMU\_、Microsoft Windows SDK ドキュメントで PORTCAPS 構造体。

## <span id="ddk_ksproperty_synth_channelgroups_ks"></span><span id="DDK_KSPROPERTY_SYNTH_CHANNELGROUPS_KS"></span>


### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

KSPROPERTY\_シンセサイザー\_CHANNELGROUPS プロパティが設定または暗証番号 (pin) のインスタンスでアクティブなチャネルのグループの数を取得する、システムによって使用されます。 チャネルのグループは各ピンのインスタンスで、0 から始まる番号が付けられます。

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
<th align="left">Set</th>
<th align="left">移行先</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>はい</p></td>
<td align="left"><p>はい</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537143" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537143)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は ULONG 型で、チャネルの数、暗証番号 (pin) がサポートのグループを指定します。 Pin をサポートしている場合*n*チャネル グループ、ピン チャネル グループは、0 から番号が*n*-1。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_シンセサイザー\_CAPS プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。 次の表では、可能性のあるエラー コードの一部を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">状態コード</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>STATUS_BUFFER_TOO_SMALL</p></td>
<td align="left"><p>バッファーが小さすぎるため、操作を完了します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_UNSUCCESSFUL</p></td>
<td align="left"><p>操作が正常に完了しませんでした。</p></td>
</tr>
</tbody>
</table>

 

チャネルのグループの詳細については、の説明を参照してください、 **IDirectMusicPort::GetNumChannelGroups**と**IDirectMusicPort::SetNumChannelGroups** Microsoft Windows SDK 内のメソッドドキュメントです。

## <span id="ddk_ksproperty_synth_latencyclock_ks"></span><span id="DDK_KSPROPERTY_SYNTH_LATENCYCLOCK_KS"></span>


### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

KSPROPERTY\_シンセサイザー\_LATENCYCLOCK プロパティは、ストリームの現在の待機時間制時刻、マスター クロックの時刻よりも大きいは常に、ミニポート ドライバーをクエリに使用します。

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
<th align="left">Set</th>
<th align="left">移行先</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>はい</p></td>
<td align="left"><p>いいえ</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537143" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537143)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>ULONGLONG</p></td>
</tr>
</tbody>
</table>

 

ULONGLONG 型とプロパティ値 (データの操作) のシンセサイザーの現在の待機時間を表します。 今回はマスター クロックに対して相対的に指定し、100 ナノ秒単位で表されます。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_シンセサイザー\_LATENCYCLOCK プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。 次の表では、可能性のあるエラー コードの一部を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">状態コード</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>STATUS_BUFFER_TOO_SMALL</p></td>
<td align="left"><p>バッファーが小さすぎるため、操作を完了します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_UNSUCCESSFUL</p></td>
<td align="left"><p>操作が正常に完了しませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_INVALID_DEVICE_REQUEST</p></td>
<td align="left"><p>このデバイスの操作が正しくありません。</p></td>
</tr>
</tbody>
</table>

 

クロックの待機時間は通常、複数のデバイス間でのオーディオ出力ストリームの同期に使用されます。

KSPROPERTY\_シンセサイザー\_LATENCYCLOCK プロパティの get 要求は、現在のマスター クロック時間に相当する遅延時間を返すようにするし、最小値は、ストリームを通過するオーディオ フィルターの待機時間を保証します。 アプリケーション プログラムを遅延に再生データを持つ現在の待機時間クロック時間リスクよりも前に再生できるオーディオ データをスケジュールします。

待機時間のクロックの詳細については、次を参照してください。

-   KSPROPERTY のディスカッション\_シンセサイザー\_LATENCYCLOCK プロパティ[待機時間のクロック](https://msdn.microsoft.com/library/windows/hardware/ff537503)します。

-   説明については、 **IDirectMusicPort::GetLatencyClock**と**IReferenceClock::GetTime** Microsoft Windows SDK のドキュメント内のメソッド。

## <span id="ddk_ksproperty_synth_portparameters_ks"></span><span id="DDK_KSPROPERTY_SYNTH_PORTPARAMETERS_KS"></span>


### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

KSPROPERTY\_シンセサイザー\_PORTPARAMETERS プロパティを使用する DirectMusic の構成パラメーターの取得を*ポート*、送信または音楽データを受信するデバイスの DirectMusic 用語であります。 (KS 用語では、DirectMusic ポートは対応しません Dmu ポート ドライバーにします。 DirectMusic フィルターでレンダリングまたはキャプチャ pin にで対応にします。)

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
<th align="left">Set</th>
<th align="left">移行先</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>はい</p></td>
<td align="left"><p>いいえ</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537143" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537143)"><strong>KSNODEPROPERTY</strong></a> + <a href="https://msdn.microsoft.com/library/windows/hardware/ff538467" data-raw-source="[&lt;strong&gt;SYNTH_PORTPARAMS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff538467)"><strong>SYNTH_PORTPARAMS</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff538467" data-raw-source="[&lt;strong&gt;SYNTH_PORTPARAMS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff538467)"><strong>SYNTH_PORTPARAMS</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ記述子 (インスタンス データ) から成る、シンセサイザー直後に続くです KSNODEPROPERTY 構造\_PORTPARAMS 構造体。 プロパティの要求を送信する前に、クライアントは、シンセサイザーに書き込むことによって、要求されたパラメーター値を指定します\_PORTPARAMS 構造体。

プロパティ値 (データの操作) が型シンセサイザーも\_PORTPARAMS します。 ミニポート ドライバーには、実際には、ポート構成に使用されるパラメーター値では、この構造が読み込まれます。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

ステータスを返す、呼び出し元が指定されているとおり DirectMusic ポートの構成に成功すると、ミニポート ドライバー、\_成功コード。 それ以外の場合、該当するエラー コードを返します。 次の表では、可能性のあるエラー状態コードの一部を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">状態コード</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>STATUS_NOT_ALL_ASSIGNED</p></td>
<td align="left"><p>操作が成功したが、ミニポート ドライバーが 1 つまたは複数の呼び出し元のプロパティの値としてマークするパラメーターの値を変更する必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_UNSUCCESSFUL</p></td>
<td align="left"><p>操作が正常に完了しませんでした。</p></td>
</tr>
</tbody>
</table>

 

これは、処理するために DirectMusic プロパティ項目の中で最も複雑です。 このプロパティには、get 要求のみがサポートされていますが、get 要求はまた、ポート パラメーターを設定します。 ポート渡しますをシンセサイザー\_プロパティ要求のプロパティ記述子と PORTPARAMS 構造体。 プロパティ値のバッファーには、プロパティの要求が付属してが get 要求であるために、バッファーは、ミニポート ドライバーから情報を取得、使用のみ。

ミニポート ドライバーはまず、シンセサイザー、コピー\_プロパティ値のバッファーをプロパティ記述子から PORTPARAMS 構造体。 次に、すべてのパラメーター値を呼び出し元が要求した (有効なものとしてマークされている) をサポートできるかどうかを確認にする必要があります。 'File.' を上書きする必要があります、ミニポート ドライバーが要求されたパラメーター値の 1 つ以上をサポートするためにできない場合は、(、シンセサイザーで\_PORTPARAMS 構造、プロパティ値のバッファーで)、要求された値これら特定のパラメーターの値を使用しています。サポートできます。

呼び出し元のシンセサイザーするかどうか、ミニポート ドライバーに変更が加えられなければ\_PORTPARAMS、呼び出し元得られるはず、呼び出し元はもともとミニポート ドライバーに送信されるプロパティ記述子では、パラメーターを正確に一致するプロパティの値。

慣例により、ドライバーも入力で設定された対応するビットがないパラメーターの値、 **dwValidParams**シンセサイザーのメンバー\_PORTPARAMS します。 これにより、呼び出し元がどのような既定値はこれらのパラメーターを使用するミニポート ドライバーを確認できます。 ミニポート ドライバーでは、wave インターフェイス デバイスを作成するために使用する実際のパラメーター値を出力します。

ミニポート ドライバーの KSPROPERTY\_シンセサイザー\_PORTPARAMETERS ハンドラーを正しくサンプル速度の変更の要求を処理するために準備する必要があります。

## <span id="ddk_ksproperty_synth_runningstats_ks"></span><span id="DDK_KSPROPERTY_SYNTH_RUNNINGSTATS_KS"></span>


### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

KSPROPERTY\_シンセサイザー\_RUNNINGSTATS プロパティは、クエリ シンセサイザーのパフォーマンス統計のミニポート ドライバーを使用します。

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
<th align="left">Set</th>
<th align="left">移行先</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>はい</p></td>
<td align="left"><p>いいえ</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537143" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537143)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff538473" data-raw-source="[&lt;strong&gt;SYNTH_STATS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff538473)"><strong>SYNTH_STATS</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は型シンセサイザーの構造体\_統計。 ミニポート ドライバーのプロパティのハンドラーは、この構造体に、以下の統計情報を書き込みます。

-   音声の再生の平均数

-   CPU 使用率

-   失われたメモの数

-   空きメモリの量

-   ピーク時のボリューム レベル

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_シンセサイザー\_RUNNINGSTATS プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。 次の表では、可能性のあるエラー コードの一部を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">状態コード</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>STATUS_BUFFER_TOO_SMALL</p></td>
<td align="left"><p>バッファーが小さすぎるため、操作を完了します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_UNSUCCESSFUL</p></td>
<td align="left"><p>操作が正常に完了しませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_INVALID_DEVICE_REQUEST</p></td>
<td align="left"><p>このデバイスの操作が正しくありません。</p></td>
</tr>
</tbody>
</table>

 

デバイスが、KSSTATE でままシンセサイザーのパフォーマンス統計が更新継続的に\_の実行の状態。 デバイスがこの状態になるたびに、統計は、ピーク時のボリュームの番号などの累積的な値をゼロにリセットされますノートが失われるのです。

詳細については、の説明を参照して、 **IDirectMusicPort::GetRunningStats**メソッドと、DMU\_Microsoft Windows SDK ドキュメントで SYNTHSTATS 構造体。

## <span id="ddk_ksproperty_synth_voicepriority_ks"></span><span id="DDK_KSPROPERTY_SYNTH_VOICEPRIORITY_KS"></span>


### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

KSPROPERTY\_シンセサイザー\_VOICEPRIORITY プロパティは、その音声キャッシュから音声をどのような優先度のミニポート ドライバーを増やす必要がある場合、MIDI シンセサイザーで特定の音声がありますを指定します。

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
<th align="left">Set</th>
<th align="left">移行先</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>はい</p></td>
<td align="left"><p>はい</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537143" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537143)"><strong>KSNODEPROPERTY</strong></a> + <a href="https://msdn.microsoft.com/library/windows/hardware/ff538452" data-raw-source="[&lt;strong&gt;SYNTHVOICEPRIORITY_INSTANCE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff538452)"><strong>SYNTHVOICEPRIORITY_INSTANCE</strong></a></p></td>
<td align="left"><p>DWORD</p></td>
</tr>
</tbody>
</table>

 

プロパティ記述子 (インスタンス データ) から成る、SYNTHVOICEPRIORITY 直後に続くです KSNODEPROPERTY 構造\_インスタンスの構造は、音声のチャネルのグループ (16 MIDI チャネルのセット) およびチャネルの数 (を指定しますグループ内)。

プロパティの値 (データの操作) は、優先順位を指定する DWORD です。 クライアントの使用、KSPROPERTY\_シンセサイザー\_、ミニポート ドライバーと音声の新しい優先順位の送信 VOICEPRIORITY プロパティの設定要求は、KSPROPERTY を使用して\_シンセサイザー\_VOICEPRIORITY プロパティの get 要求ミニポート ドライバーから音声の現在の優先順位を取得します。

**音声の優先順位**

Dmusprop.h のヘッダー ファイルでは、次のチャネル グループの優先順位が定義されています。

```cpp
  DAUD_CRITICAL_VOICE_PRIORITY
  DAUD_HIGH_VOICE_PRIORITY
  DAUD_STANDARD_VOICE_PRIORITY
  DAUD_LOW_VOICE_PRIORITY
  DAUD_PERSIST_VOICE_PRIORITY
```

上記の一覧は、一覧の上部にある最も高い優先順位と下部には、最低で並んでいます。 これらの優先順位は、チャネルのグループ内の各チャネルの音声の優先順位に到着するチャネルの優先順位のオフセットを持つ論理和が。 結果として得られる優先度は、get および set プロパティ要求で渡されます。

前述のチャネル グループの優先順位値は、チャネルの優先順位のオフセットに比べると大規模なです。 チャネル グループの優先順位の発生またはチャネル グループ内のチャネルの相対的な優先度を変更することがなく他のチャネルのグループの基準とした全体のチャンネルのグループの優先度を下げて、その変更になります。

### <a name="span-iddefaultprioritiesspanspan-iddefaultprioritiesspan-default-priorities"></a><span id="default_priorities"></span><span id="DEFAULT_PRIORITIES"></span> 既定の優先順位

シンセサイザーのミニポート ドライバーを作成すると、その音声のそれぞれに既定の優先順位が割り当てられます。 既定値の定義は次のとおりです。

-   既定では優先順位はチャネルのグループ間で等しくなります。 つまり、たとえば、チャネル グループ 1 の 5 そのチャネルがチャネル グループ 2 のチャネル 5 と同じ優先順位。

-   DLS レベル 1 の仕様に従って channel 10 (MIDI パーカッション チャネル) は、1 ~ 9、および 11 ~ 16 の後に、最高の優先順位を持ちます。

ヘッダー ファイル Dmusprop.h では、次の優先度のオフセットを定義します。

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

オフセットの前のリストの順序は、一覧の上部にある優先順位が高い。 ヘッダー ファイル Dmusprop.h ダウドとオフセットをこれらの各ビットごとの Or では、各チャネル グループ内のチャネルの既定の優先順位も定義します\_標準\_音声\_優先順位。 たとえば、次の定義には、各チャネル グループ チャネル 1 の既定の優先順位が与えられます。

```cpp
  #define DAUD_CHAN1_DEF_VOICE_PRIORITY \
    (DAUD_STANDARD_VOICE_PRIORITY | DAUD_CHAN1_VOICE_PRIORITY_OFFSET)
```

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_シンセサイザー\_VOICEPRIORITY プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。 次の表では、可能性のあるエラー コードの一部を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">状態コード</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>STATUS_BUFFER_TOO_SMALL</p></td>
<td align="left"><p>バッファーが小さすぎるため、操作を完了します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_UNSUCCESSFUL</p></td>
<td align="left"><p>操作が正常に完了しませんでした。</p></td>
</tr>
</tbody>
</table>

 

音声の優先順位の詳細については、の説明を参照してください、 **IDirectMusicPort::GetChannelPriority**と**IDirectMusicPort::SetChannelPriority** Microsoft Windows SDK 内のメソッドドキュメントです。

## <span id="ddk_ksproperty_synth_volume_ks"></span><span id="DDK_KSPROPERTY_SYNTH_VOLUME_KS"></span>


### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

KSPROPERTY\_シンセサイザー\_ボリュームのプロパティを取得またはシンセサイザー デバイスのボリューム レベルを設定します。

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
<th align="left">Set</th>
<th align="left">移行先</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>はい</p></td>
<td align="left"><p>はい</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564262" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564262)"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p>長い</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (データの操作) は LONG 型のシンセサイザー デバイスのボリューム レベルを指定します。 ボリュームの設定は、1/100ths デシベル単位で指定されます。 ミニポート ドライバーは、する必要がありますか、そのボリュームを変更または要求が、プロパティを取得または設定があるかによって、そのボリュームをレポートします。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_シンセサイザー\_ボリューム プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。 次の表では、可能性のあるエラー コードの一部を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">状態コード</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>STATUS_BUFFER_TOO_SMALL</p></td>
<td align="left"><p>バッファーが小さすぎるため、操作を完了します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_UNSUCCESSFUL</p></td>
<td align="left"><p>操作が正常に完了しませんでした。</p></td>
</tr>
</tbody>
</table>

 

## <span id="ddk_ksproperty_synth_volumeboost_ks"></span><span id="DDK_KSPROPERTY_SYNTH_VOLUMEBOOST_KS"></span>


### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

KSPROPERTY\_シンセサイザー\_VOLUMEBOOST プロパティをシンセサイザー デバイスのボリュームがブーストされる量を指定します。

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
<th align="left">Set</th>
<th align="left">移行先</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>はい</p></td>
<td align="left"><p>はい</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537143" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537143)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>長い</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (データの操作) は LONG 型のミックス段階の後のオーディオ信号を促進する量を指定します。 これは、すべての音声アーティキュレーション後のシンセサイザーの最終的な出力に追加するボリュームの量との混在が完了します。 ボリューム boost 量は、1/100ths デシベルで指定されます。 この値は、正または負の値を指定できます。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_シンセサイザー\_VOLUMEBOOST プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。 次の表では、可能性のあるエラー コードの一部を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">状態コード</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>STATUS_BUFFER_TOO_SMALL</p></td>
<td align="left"><p>バッファーが小さすぎるため、操作を完了します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_UNSUCCESSFUL</p></td>
<td align="left"><p>操作が正常に完了しませんでした。</p></td>
</tr>
</tbody>
</table>

 

他のブーストを出力に追加する必要がありますはされません。 シンセサイザーは、アーティキュレーションの厳密な DLS レベル 1 の規則に従う必要があります。

このプロパティは、システムでは、その他のオーディオ出力のシンセサイザーの量を均等に使用され、すべてのデバイスで一貫した方法で boost 金額が解釈したがって必要があります。

 

 





