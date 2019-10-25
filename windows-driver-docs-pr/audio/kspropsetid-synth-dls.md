---
title: KSPROPSETID\_シンセサイザー\_Dls
description: KSPROPSETID\_シンセサイザー\_Dls
ms.assetid: 8d6038bf-1ec4-4120-9815-d1e6b7994f33
keywords:
- KSPROPSETID_Synth_Dls
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 83f61b42a505f7c2f918a521fb060cdbad07043b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832667"
---
# <a name="kspropsetid_synth_dls"></a>KSPROPSETID\_シンセサイザー\_Dls


## <span id="ddk_kspropsetid_synth_dls_ks"></span><span id="DDK_KSPROPSETID_SYNTH_DLS_KS"></span>


`KSPROPSETID_Synth_Dls` プロパティセットには、DLS サンプルおよび音色を MIDI シンセサイザーにダウンロードするために使用されるプロパティが含まれています。 これらは、DirectMusic フィルターの DirectMusic ピン上のシンセサイザーノード ([**KSNODETYPE\_シンセサイザー**](ksnodetype-synthesizer.md)) のプロパティです (「 [MIDI フィルターと directmusic フィルター](https://docs.microsoft.com/windows-hardware/drivers/audio/midi-and-directmusic-filters)」を参照してください)。

このセクションでは、DLS データを含むメモリの "チャンク" をダウンロードしてアンロードする方法に関して、これらのプロパティの動作について説明します。 ダウンロードしたインストルメントの実際の形式と wave データのチャンクは、Microsoft Windows SDK のドキュメントに記載されている低レベルの DLS の説明で指定されています。

DLS のダウンロードとアンロードは、pin の存在中にいつでも発生する可能性があります。 DirectMusic イベントとは異なり、これらはタイムスタンプではなく、できるだけ早く処理する必要があります。

このセクションでは、DLS リソース (つまり、ただ1つのリソース) という用語は、DLS インストルメントチャンクまたは DLS wave チャンクを指します。 システムは、すべての DLS リソースの参照カウントを適切に管理します。

-   クライアントが wave を参照する最後のインストルメントをアンロードすると、システムは wave をアンロードするための呼び出しを自動的に生成します。

-   逆に、システムは、wave を参照する最後のインストルメントをクライアントがアンロードするまで、呼び出しを延期して wave をアンロードします。

このセットのプロパティ項目は、ヘッダーファイル Dマス\_に定義されているように、KSK プロパティシンセサイザー\_DLS 列挙値によって指定されます。

## <span id="ddk_ksproperty_synth_dls_append_ks"></span><span id="DDK_KSPROPERTY_SYNTH_DLS_APPEND_KS"></span>


### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

KSK プロパティ\_シンセサイザー\_DLS\_APPEND プロパティは、クライアントがシンセサイザーにダウンロードする各バッファー内の DLS データに追加する予約済みストレージ領域の量を指定します。

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
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) の型は ULONG で、ダウンロードされた各 DLS data buffer の最後にミニポートドライバーが自身で使用するために予約する必要があるバイト数を指定します。 次に、クライアントは、ダウンロードされたデータの終了後に要求されたバイト数を格納するのに十分な大きさの各ダウンロードバッファーを割り当てます。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_シンセサイザー\_DLS\_APPEND プロパティ要求は正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。 次の表に、考えられるエラーコードを示します。

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
<td align="left"><p>STATUS_UNSUCCESSFUL</p></td>
<td align="left"><p>操作は正常に完了しませんでした。</p></td>
</tr>
</tbody>
</table>

 

これらの追加のバイトは、サンプル補間を簡略化するために、配置要件に余分な埋め込みが必要なドライバーや、サンプルの開始をレプリケートするドライバーを対象としています。

## <span id="ddk_ksproperty_synth_dls_compact_ks"></span><span id="DDK_KSPROPERTY_SYNTH_DLS_COMPACT_KS"></span>


### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

KSK プロパティ\_シンセサイザー\_DLS\_COMPACT プロパティは、シンセサイザーが無料サンプルメモリの最大チャンクを利用できるようにするための要求です。

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
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>なし</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) がこのプロパティに関連付けられていません。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_シンセサイザー\_DLS\_COMPACT プロパティ要求は正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。 次の表に、考えられるエラーコードを示します。

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
<td align="left"><p>STATUS_UNSUCCESSFUL</p></td>
<td align="left"><p>操作は正常に完了しませんでした。</p></td>
</tr>
</tbody>
</table>

 

このプロパティのハンドラーの実装では、再生を中断できません。

詳細については、Microsoft Windows SDK のドキュメントで**IDirectMusicPort:: Compact**メソッドの説明を参照してください。

## <span id="ddk_ksproperty_synth_dls_download_ks"></span><span id="DDK_KSPROPERTY_SYNTH_DLS_DOWNLOAD_KS"></span>


### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

KSK プロパティ\_シンセサイザー\_DLS\_DOWNLOAD プロパティは、DLS データをシンセサイザーにダウンロードするために使用されます。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a> + <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusprop/ns-dmusprop-_synth_buffer" data-raw-source="[&lt;strong&gt;SYNTH_BUFFER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusprop/ns-dmusprop-_synth_buffer)"> <strong>SYNTH_BUFFER</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusprop/ns-dmusprop-_synthdownload" data-raw-source="[&lt;strong&gt;SYNTHDOWNLOAD&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusprop/ns-dmusprop-_synthdownload)"><strong>SYNTHDOWNLOAD</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ記述子 (インスタンスデータ) は、KSNODEPROPERTY 構造体で構成されます。この構造体には、すぐ後に、ダウンロードする DLS データバッファーの場所とサイズを指定する、\_バッファー構造が含まれます。

プロパティ値 (操作データ) は、SYNTHDOWNLOAD 構造体です。 ミニポートドライバーは、この構造体の次の情報を返します。

-   ダウンロードされた DLS データを一意に識別するためにミニポートドライバーが生成するハンドル。 このクライアントは、このハンドルを保存し、後でデータをアンロードするために使用します (「 [**Ksk プロパティ\_シンセサイザー\_DLS\_unload**](https://docs.microsoft.com/previous-versions/ff537398(v=vs.85)))」を参照してください。

-   プロパティ要求の完了後に、クライアントが DLS データを格納しているバッファーを解放できるかどうかを示すブール値。 ミニポートドライバーによって、DLS データの独自のコピーが作成された場合、クライアントはバッファーを解放できます。 それ以外の場合、ミニポートドライバーがクライアントの元の DLS データバッファーを引き続き使用する場合、クライアントは、ミニポートドライバーが DLS データをアンロードするまでバッファーを解放しないようにする必要があります。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_シンセサイザー\_DLS\_DOWNLOAD property 要求は正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。 次の表に、考えられるエラーコードを示します。

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
<td align="left"><p>STATUS_NO_MEMORY</p></td>
<td align="left"><p>この要求を完了するために使用できるメモリがありません。</p></td>
</tr>
</tbody>
</table>

 

詳細については、Microsoft Windows SDK のドキュメントの**IDirectMusicPort::D ownloadinstrument**メソッドの説明を参照してください。

**例**

KSK プロパティ\_シンセサイザー\_DLS\_DOWNLOAD property 要求では、ユーザーメモリアドレスを持つ DLS ダウンロードデータの場所を指定します。 ミニポートドライバーは、アクセスを試みる前に、DLS データを含むユーザーメモリをプローブしてロックする必要があります。 次のコード例は、これを行う方法を示しています。

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


### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

KSK プロパティ\_シンセサイザー\_DLS\_UNLOAD プロパティは、以前にダウンロードされた DLS データリソースをアンロードします。

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
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>扱え</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) はハンドル型であり、解放されるダウンロード済みの DLS データリソースのハンドルを格納します。 これは、以前の[**ksproperty\_シンセサイザー\_dls**](https://docs.microsoft.com/previous-versions/ff537396(v=vs.85))を識別するためにミニポートドライバーによって生成されたハンドルで、get property 要求をダウンロード\_ます。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_シンセサイザー\_DLS\_UNLOAD プロパティ要求は正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。 次の表に、考えられるエラーコードを示します。

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
<td align="left"><p>あります</p></td>
<td align="left"><p>操作は後で完了します。</p></td>
</tr>
</tbody>
</table>

 

DLS データを使用するノートが再生されないので、ミニポートドライバーは DLS データをアンロードする必要があります。 \_の KSK プロパティの時点で、DLS データリソースに関連付けられているメモリをシンセサイザーが解放できない場合は、\_DLS によってプロパティのアンロード\_アンロードされます。プロパティの非同期完了を使用して、後で要求を完了することができます.

DLS data リソースをアンロードした後で、リソースを使用するノートオンイベントがシンセサイザーによって受信された場合、新しい DLS data リソースが一時的にダウンロードされていない限り、ミニポートドライバーはイベントを無視する必要があります。

詳細については、Microsoft Windows SDK のドキュメントの**IDirectMusicPort:: UnloadInstrument**メソッドの説明を参照してください。

## <span id="ddk_ksproperty_synth_dls_waveformat_ks"></span><span id="DDK_KSPROPERTY_SYNTH_DLS_WAVEFORMAT_KS"></span>


### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

KSK プロパティ\_シンセサイザー\_DLS\_WAVEFORMAT プロパティを使用して、シンセサイザーに出力 wave 形式のクエリを実行します。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/mmreg/ns-mmreg-twaveformatex" data-raw-source="[&lt;strong&gt;WAVEFORMATEX&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/mmreg/ns-mmreg-twaveformatex)"><strong>WAVEFORMATEX</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は WAVEFORMATEX 型で、シンセサイザーの出力ストリームの波形式を指定します。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_シンセサイザー\_DLS\_WAVEFORMAT property 要求は正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。 次の表に、考えられるエラーコードを示します。

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
</tbody>
</table>

 

**Sizeof**(WAVEFORMATEX) バイトのプロパティ値バッファーは、すべての wave 形式に対して十分な大きさではない可能性があります。 たとえば、マルチチャネル形式では、 **sizeof**([**WAVEFORMATEXTENSIBLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-waveformatextensible)) バイトのバッファーが必要です。 プロパティ要求によってステータスコード\_返された状態コードが\_\_小さすぎる場合、クライアントは、ミニポートドライバーが出力するプロパティ値のサイズを確認し、大きいバッファーを割り当ててから、2番目の要求を送信できます。

詳細については、Microsoft Windows SDK のドキュメントの**IDirectMusicPort:: GetFormat**メソッドの説明を参照してください。

 

 





