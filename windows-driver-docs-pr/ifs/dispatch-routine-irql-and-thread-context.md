---
title: ディスパッチ ルーチン IRQL とスレッド コンテキスト
description: ディスパッチ ルーチン IRQL とスレッド コンテキスト
ms.assetid: 95f3a976-c97a-4c8a-979b-14a0ddd823a2
keywords:
- IRP ディスパッチルーチン WDK ファイルシステム、IRQL
- IRP ディスパッチルーチン WDK ファイルシステム、スレッドコンテキスト
- 非任意のスレッドコンテキスト WDK ファイルシステム
- スレッドコンテキスト WDK ファイルシステム
- 任意のスレッドコンテキスト WDK ファイルシステム
- IRQLs WDK ファイルシステム
ms.date: 01/22/2020
ms.localizationpriority: medium
ms.openlocfilehash: b00508f65d19bb0f46776781a84ebc8a9e32ae28
ms.sourcegitcommit: 8dd886d4be2c21c6b19ace5ff0521b1bcaf5b383
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/22/2020
ms.locfileid: "76521802"
---
# <a name="dispatch-routine-irql-and-thread-context"></a>ディスパッチ ルーチン IRQL とスレッド コンテキスト


## <span id="ddk_dispatch_routine_irql_and_thread_context_if"></span><span id="DDK_DISPATCH_ROUTINE_IRQL_AND_THREAD_CONTEXT_IF"></span>


次の表は、ファイルシステムフィルタードライバーのディスパッチルーチンの IRQL とスレッドコンテキストの要件をまとめたものです。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ディスパッチルーチン</th>
<th align="left">呼び出し元の最大 IRQL:</th>
<th align="left">呼び出し元のスレッドコンテキスト:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>クリーンアップ</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>任意</p></td>
</tr>
<tr class="even">
<td align="left"><p>Close</p></td>
<td align="left"><p>APC_LEVEL</p></td>
<td align="left"><p>勝手</p></td>
</tr>
<tr class="odd">
<td align="left"><p>[作成]</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>任意</p></td>
</tr>
<tr class="even">
<td align="left"><p>DeviceControl (ページング i/o を除く)</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>任意</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DeviceControl (ページング i/o パス)</p></td>
<td align="left"><p>APC_LEVEL</p></td>
<td align="left"><p>勝手</p></td>
</tr>
<tr class="even">
<td align="left"><p>DirectoryControl</p></td>
<td align="left"><p>APC_LEVEL</p></td>
<td align="left"><p>勝手</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FlushBuffers</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>任意</p></td>
</tr>
<tr class="even">
<td align="left"><p>FsControl (ページング i/o を除く)</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>任意</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FsControl (ページング i/o パス)</p></td>
<td align="left"><p>APC_LEVEL</p></td>
<td align="left"><p>勝手</p></td>
</tr>
<tr class="even">
<td align="left"><p>LockControl</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>任意</p></td>
</tr>
<tr class="odd">
<td align="left"><p>全て</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>勝手</p></td>
</tr>
<tr class="even">
<td align="left"><p>Quer</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>任意</p></td>
</tr>
<tr class="odd">
<td align="left"><p>QueryInformation</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>任意</p></td>
</tr>
<tr class="even">
<td align="left"><p>QueryQuota</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>任意</p></td>
</tr>
<tr class="odd">
<td align="left"><p>QuerySecurity</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>任意</p></td>
</tr>
<tr class="even">
<td align="left"><p>QueryVolumeInfo</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>任意</p></td>
</tr>
<tr class="odd">
<td align="left"><p>読み取り (ページング i/o を除く)</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>任意</p></td>
</tr>
<tr class="even">
<td align="left"><p>読み取り (ページング i/o パス)</p></td>
<td align="left"><p>APC_LEVEL</p></td>
<td align="left"><p>勝手</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SetEa</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>任意</p></td>
</tr>
<tr class="even">
<td align="left"><p>SetInformation</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>任意</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SetQuota</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>任意</p></td>
</tr>
<tr class="even">
<td align="left"><p>SetSecurity</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>任意</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SetVolumeInfo</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>任意</p></td>
</tr>
<tr class="even">
<td align="left"><p>シャットダウン</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>勝手</p></td>
</tr>
<tr class="odd">
<td align="left"><p>書き込み (ページング i/o を除く)</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>任意</p></td>
</tr>
<tr class="even">
<td align="left"><p>書き込み (ページング i/o パス)</p></td>
<td align="left"><p>APC_LEVEL</p></td>
<td align="left"><p>勝手</p></td>
</tr>
</tbody>
</table>

 

 

 




