---
title: シンボル状態の省略形
description: シンボル状態の省略形
ms.assetid: 198453f2-fc9a-4313-875e-ac963b843df9
keywords:
- deferred (シンボルの状態の省略形)
- (シンボルの状態の省略形) の遅延
- (シンボルの状態の省略形)
- T (シンボルの状態の省略形)
- C (シンボルの状態の省略形)
- DIA (シンボルの状態の省略形)
- Export (シンボルの状態の省略形)
- PERF (シンボルの状態の省略形)
- PDB (シンボルの状態の省略形)
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7aadee45618c5fddfc3641d2c049b55c719e877
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335492"
---
# <a name="symbol-status-abbreviations"></a>シンボル状態の省略形


## <span id="ddk_symbol_status_abbreviations_dbg"></span><span id="DDK_SYMBOL_STATUS_ABBREVIATIONS_DBG"></span>


使用してシンボル ファイルの種類とその読み込み状態を決定できます、 [ **lm (読み込まれたモジュールの一覧)** ](lm--list-loaded-modules-.md)コマンド、 [ **! lmi** ](-lmi.md)拡張機能、または WinDbg の[デバッグ |モジュール](debug---modules.md)メニュー コマンド。

これらのそれぞれには、読み込まれたモジュールと、シンボルに関する情報が表示されます。

次の省略形は、これらのコマンドによって生成された表示で使用されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">省略形</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>遅延</strong></p></td>
<td align="left"><p>モジュールが読み込まれたが、デバッガーがシンボルを読み込むには試行されません。 必要なときにシンボルが読み込まれます。 参照してください<a href="deferred-symbol-loading.md" data-raw-source="[Deferred Symbol Loading](deferred-symbol-loading.md)">シンボルの読み込みの遅延</a>詳細についてはします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>#</strong></p></td>
<td align="left"><p>シンボル ファイルと実行可能ファイル、そのタイムスタンプかチェックサムの不一致があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>T</strong></p></td>
<td align="left"><p>タイムスタンプが見つからないか、アクセスできない、または 0 に等しいです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>C</strong></p></td>
<td align="left"><p>チェックサムが見つからないか、アクセスできない、または 0 に等しいです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>DIA</strong></p></td>
<td align="left"><p>シンボル ファイルは、デバッグ インターフェイスへのアクセス (DIA) 経由で読み込まれました。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>[エクスポート]</strong></p></td>
<td align="left"><p>シンボル情報は、バイナリ ファイルのエクスポート テーブルから抽出されたため、実際のシンボル ファイルがありませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>M</strong></p></td>
<td align="left"><p>シンボル ファイルと実行可能ファイル、そのタイムスタンプかチェックサムの不一致があります。 ただし、シンボル ファイルは、シンボルのオプション設定が原因か読み込まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>パフォーマンス</strong></p></td>
<td align="left"><p>このバイナリを含む<a href="debugging-performance-optimized-code.md" data-raw-source="[performance-optimized code](debugging-performance-optimized-code.md)">コードのパフォーマンスが最適化された</a>します。 標準アドレス算術演算では、正しい結果が得られない可能性があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>削除</strong></p></td>
<td align="left"><p>デバッグ情報がイメージ ファイルから削除されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>PDB ファイル</strong></p></td>
<td align="left"><p>シンボルは .pdb 形式です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>COFF</strong></p></td>
<td align="left"><p>シンボルは、オブジェクト ファイル形式 (COFF) 記号の表示形式では共通です。</p></td>
</tr>
</tbody>
</table>

 

 

 





