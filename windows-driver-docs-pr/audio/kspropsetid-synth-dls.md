---
title: KSPROPSETID\_シンセサイザー\_Dls
description: KSPROPSETID\_シンセサイザー\_Dls
ms.assetid: 8d6038bf-1ec4-4120-9815-d1e6b7994f33
keywords:
- KSPROPSETID_Synth_Dls
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 469dd11d27cd70288d9dd8e0d6f4a632a0b6dc7a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360476"
---
# <a name="kspropsetidsynthdls"></a>KSPROPSETID\_シンセサイザー\_Dls


## <span id="ddk_kspropsetid_synth_dls_ks"></span><span id="DDK_KSPROPSETID_SYNTH_DLS_KS"></span>


`KSPROPSETID_Synth_Dls` DLS サンプルと instruments MIDI シンセサイザーをダウンロードに使用されるプロパティがプロパティ セットに含まれています。 これらはシンセサイザー ノードのプロパティ ([**KSNODETYPE\_シンセサイザー**](ksnodetype-synthesizer.md)) DirectMusic フィルターの DirectMusic ピン (を参照してください[MIDI と DirectMusic フィルター](https://docs.microsoft.com/windows-hardware/drivers/audio/midi-and-directmusic-filters)).

このセクションでは、ダウンロードおよび配布リストのデータを格納しているメモリの"チャンク"単位をアンロードする方法に関してこれらのプロパティの動作について説明します。 ダウンロードしたツールと wave データ チャンクの実際の形式は、Microsoft Windows SDK ドキュメントでの低レベルの DL ディスカッションで指定されます。

DLS がダウンロードされ、暗証番号 (pin) の存在の中にいつでも発生することがアンロードされます。 DirectMusic のイベントとは異なり、タイム スタンプされていないと、できるだけ早く処理する必要があります。

このセクションで、用語 DLS のリソース、または単なるリソース、DLS インストルメント化のチャンクまたは DLS wave チャンクのいずれかを意味します。 システムは正しく配布リストのすべてのリソースの参照カウントを保持します。

-   クライアントは、波を参照する最後のインストルメント化をアンロードするときに自動的にアンロード、wave への呼び出しが生成されます。

-   逆に、システムは、クライアント、wave を参照する最後のインストルメント化がアンロードされるまで、波をアンロードする呼び出しを延期します。

このセット内のプロパティ項目が KSPROPERTY によって指定された\_シンセサイザー\_DLS 列挙値では、ヘッダーで定義されているファイル Dmusprop.h します。

## <span id="ddk_ksproperty_synth_dls_append_ks"></span><span id="DDK_KSPROPERTY_SYNTH_DLS_APPEND_KS"></span>


### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

KSPROPERTY\_シンセサイザー\_DLS\_追加プロパティをシンセサイザーをダウンロードする各バッファーの DL データにクライアントを追加する予約済みの記憶域スペースの量を指定します。

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
<td align="left"><p>いいえ</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は ULONG 型で、ミニポート ドライバーは、各ダウンロードした DLS データ バッファーの末尾に使用するために予約する必要のあるバイト数を指定します。 クライアントは、ダウンロードされたデータの終了後、要求されたバイト数を格納するのに十分な大きさにするには、各ダウンロード バッファーを割り当てます。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_シンセサイザー\_DLS\_追加プロパティの要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。 次の表では、可能性のあるエラー コードの一部を示します。

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
<td align="left"><p>STATUS_UNSUCCESSFUL</p></td>
<td align="left"><p>操作が正常に完了しませんでした。</p></td>
</tr>
</tbody>
</table>

 

これらの追加のバイトは、余分なスペースを配置要件またはサンプルの補間を簡略化するため、サンプルの開始をレプリケートする必要があるドライバーを意図しています。

## <span id="ddk_ksproperty_synth_dls_compact_ks"></span><span id="DDK_KSPROPERTY_SYNTH_DLS_COMPACT_KS"></span>


### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

KSPROPERTY\_シンセサイザー\_DLS\_COMPACT プロパティは無料のサンプルのメモリの最大の可能なチャンクを使用できるようにするシンセサイザー要求です。

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
<td align="left"><p>X</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>なし</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、このプロパティに関連付けではありません。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_シンセサイザー\_DLS\_COMPACT プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。 次の表では、可能性のあるエラー コードの一部を示します。

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
<td align="left"><p>STATUS_UNSUCCESSFUL</p></td>
<td align="left"><p>操作が正常に完了しませんでした。</p></td>
</tr>
</tbody>
</table>

 

このプロパティのハンドラーの実装では、再生が中断しない必要があります。

詳細については、の説明を参照して、 **IDirectMusicPort::Compact** Microsoft Windows SDK のドキュメント内のメソッド。

## <span id="ddk_ksproperty_synth_dls_download_ks"></span><span id="DDK_KSPROPERTY_SYNTH_DLS_DOWNLOAD_KS"></span>


### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

KSPROPERTY\_シンセサイザー\_DLS\_DLS データ シンセサイザーをダウンロードするダウンロード プロパティを使用します。

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
<td align="left"><p>いいえ</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong> </a> + <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusprop/ns-dmusprop-_synth_buffer" data-raw-source="[&lt;strong&gt;SYNTH_BUFFER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusprop/ns-dmusprop-_synth_buffer)"> <strong>SYNTH_BUFFER</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusprop/ns-dmusprop-_synthdownload" data-raw-source="[&lt;strong&gt;SYNTHDOWNLOAD&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusprop/ns-dmusprop-_synthdownload)"><strong>SYNTHDOWNLOAD</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ記述子 (インスタンス データ) から成る、シンセサイザー直後に続くです KSNODEPROPERTY 構造\_バッファーの構造は、ダウンロードされる DLS データ バッファーのサイズと場所を指定します。

プロパティの値 (データの操作) は、SYNTHDOWNLOAD 構造です。 ミニポート ドライバーは、この構造体で、次の情報で渡します戻る。

-   ミニポート ドライバーを生成、ダウンロードした DLS データを一意に識別するハンドル。 このクライアントがこのハンドルを保存して、データのアンロード後で使用する必要があります (を参照してください[ **KSPROPERTY\_シンセサイザー\_DLS\_アンロード**](https://docs.microsoft.com/previous-versions/ff537398(v=vs.85)))。

-   クライアントがプロパティ要求が完了した後、DLS データを含むバッファーを解放できるかどうかを示すブール値。 ミニポート ドライバーに DLS データのコピーが行われた場合、クライアントは、バッファーを解放できます。 それ以外の場合、クライアントの元の DL データ バッファーを使用するミニポート ドライバーが引き続き発生する場合は、クライアントが解放バッファーでする必要があります、ミニポート ドライバー DLS データがアンロードされるまで。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_シンセサイザー\_DLS\_プロパティのダウンロード要求のステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。 次の表では、可能性のあるエラー コードの一部を示します。

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
<td align="left"><p>STATUS_NO_MEMORY</p></td>
<td align="left"><p>この要求を完了するメモリがありません。</p></td>
</tr>
</tbody>
</table>

 

詳細については、の説明を参照してください、 **IDirectMusicPort::DownloadInstrument** Microsoft Windows SDK のドキュメント内のメソッド。

**例**

KSPROPERTY\_シンセサイザー\_DLS\_ダウンロード プロパティ要求では、DL の場所、ユーザーのメモリ アドレスを使用してデータをダウンロードするを指定します。 ミニポート ドライバーは、プローブし、DLS データへのアクセスを試行する前に格納しているユーザーのメモリをロックする必要があります。 次のコード例では、これを行う方法を示します。

```cpp
  NTSTATUS Status = STATUS_UNSUCCESSFUL;
  PSYNTH_BUFFER pDlsBuffer = (PSYNTH_BUFFER)pRequest->Instance;
  PMDL pMdl = IoAllocateMdl(pDlsBuffer->BufferAddress, pDlsBuffer->BufferSize,
                            FALSE, FALSE, NULL);
  if (pMdl)
  {
      __try
      {
          MmProbeAndLockPages(pMdl, KernelMode, IoReadAccess);
          PVOID pvUserData = MmGetSystemAddressForMdlSafe(pMdl, NormalPagePriority);
 
         // do something with the data here
      }
      __except (EXCEPTION_EXECUTE_HANDLER)
      {
          Status = GetExceptionCode();
      }
 
      MmUnlockPages(pMdl);
      IoFreeMdl(pMdl);
  }
  else
  {
      Status = STATUS_NO_MEMORY;
  }
```

## <span id="ddk_ksproperty_synth_dls_unload_ks"></span><span id="DDK_KSPROPERTY_SYNTH_DLS_UNLOAD_KS"></span>


### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

KSPROPERTY\_シンセサイザー\_DLS\_アンロード プロパティは、以前ダウンロードした DLS データ リソースをアンロードします。

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
<td align="left"><p>X</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>ハンドル</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) はハンドル型のダウンロードした DLS データ リソースを解放するにはのハンドルを格納します。 これは、以前の DL データを識別するために、ミニポート ドライバーが生成されたハンドル[ **KSPROPERTY\_シンセサイザー\_DLS\_ダウンロード**](https://docs.microsoft.com/previous-versions/ff537396(v=vs.85))プロパティの get 要求.

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_シンセサイザー\_DLS\_アンロード プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。 次の表では、可能性のあるエラー コードの一部を示します。

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
<td align="left"><p>STATUS_PENDING</p></td>
<td align="left"><p>後で、操作を行います。</p></td>
</tr>
</tbody>
</table>

 

DLS データを再生するノートが使用できないがあるとすぐに、ミニポート ドライバーは DLS データをアンロードする必要があります。 シンセサイザーで時、KSPROPERTY の DL データ リソースに関連付けられているメモリを解放することがないかどうか\_シンセサイザー\_DLS\_非同期プロパティの入力候補を使用して、[完了]、アンロード プロパティ設定を要求します後で要求します。

DLS データ リソースをアンロードした後は、シンセサイザーはリソースを使用するメモでイベントを受信する場合は、ミニポート ドライバーは、それまでの間に新しい DLS データ リソースがダウンロードされている場合を除き、イベントを無視する必要があります。

詳細については、の説明を参照してください、 **IDirectMusicPort::UnloadInstrument** Microsoft Windows SDK のドキュメント内のメソッド。

## <span id="ddk_ksproperty_synth_dls_waveformat_ks"></span><span id="DDK_KSPROPERTY_SYNTH_DLS_WAVEFORMAT_KS"></span>


### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

KSPROPERTY\_シンセサイザー\_DLS\_WAVEFORMAT プロパティを使用して、その出力 wave 形式のシンセサイザーのクエリを実行します。

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
<td align="left"><p>いいえ</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/mmreg/ns-mmreg-twaveformatex" data-raw-source="[&lt;strong&gt;WAVEFORMATEX&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/mmreg/ns-mmreg-twaveformatex)"><strong>WAVEFORMATEX</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) では、型 WAVEFORMATEX を wave 形式のシンセサイザーの出力ストリームを指定します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_シンセサイザー\_DLS\_WAVEFORMAT プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。 次の表では、可能性のあるエラー コードの一部を示します。

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
</tbody>
</table>

 

プロパティ値のバッファー **sizeof**すべては wave 形式の (WAVEFORMATEX) バイトは十分な大きさできません。 たとえば、マルチ チャネルの形式には、バッファーが必要です。 **sizeof**([**WAVEFORMATEXTENSIBLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-waveformatextensible)) バイトです。 かどうかプロパティ要求が状態のステータス コードを返します\_バッファー\_すぎます\_小さな、クライアントは、ミニポート ドライバーを出力するプロパティ値のサイズを確認より大きなバッファーを割り当て、および 2 番目の要求を送信します。

詳細については、の説明を参照して、 **IDirectMusicPort::GetFormat** Microsoft Windows SDK のドキュメント内のメソッド。

 

 





