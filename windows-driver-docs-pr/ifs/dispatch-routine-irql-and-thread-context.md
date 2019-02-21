---
title: ディスパッチの日常的な IRQL とスレッドのコンテキスト
description: ディスパッチの日常的な IRQL とスレッドのコンテキスト
ms.assetid: 95f3a976-c97a-4c8a-979b-14a0ddd823a2
keywords:
- IRP ディスパッチ ルーチン WDK ファイル システム、IRQL
- IRP ディスパッチ ルーチン WDK ファイル システム、スレッド コンテキスト
- nonarbitrary スレッド コンテキスト WDK ファイル システム
- WDK のファイル システムのスレッド コンテキスト
- 任意のスレッド コンテキスト WDK ファイル システム
- Irql WDK ファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d9bcc852b2ee0921f2985c02f3778f91aeaaf21
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530643"
---
# <a name="dispatch-routine-irql-and-thread-context"></a>ディスパッチの日常的な IRQL とスレッドのコンテキスト


## <span id="ddk_dispatch_routine_irql_and_thread_context_if"></span><span id="DDK_DISPATCH_ROUTINE_IRQL_AND_THREAD_CONTEXT_IF"></span>


次の表では、ファイル システム フィルター ドライバーのディスパッチ ルーチンの IRQL とスレッド コンテキストの要件をまとめたものです。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ディスパッチ ルーチン</th>
<th align="left">呼び出し元&#39;s IRQL:</th>
<th align="left">呼び出し元&#39;s スレッド コンテキスト。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>クリーンアップ</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>Nonarbitrary</p></td>
</tr>
<tr class="even">
<td align="left"><p>Close</p></td>
<td align="left"><p>APC_LEVEL</p></td>
<td align="left"><p>任意</p></td>
</tr>
<tr class="odd">
<td align="left"><p>作成</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>Nonarbitrary</p></td>
</tr>
<tr class="even">
<td align="left"><p>デバイス (I/O のページング) を除く</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>Nonarbitrary</p></td>
</tr>
<tr class="odd">
<td align="left"><p>デバイス (ページング I/O パス)</p></td>
<td align="left"><p>APC_LEVEL</p></td>
<td align="left"><p>任意</p></td>
</tr>
<tr class="even">
<td align="left"><p>DirectoryControl</p></td>
<td align="left"><p>APC_LEVEL</p></td>
<td align="left"><p>任意</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FlushBuffers</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>Nonarbitrary</p></td>
</tr>
<tr class="even">
<td align="left"><p>(I/O のページング) を除く FsControl</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>Nonarbitrary</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FsControl (ページング I/O パス)</p></td>
<td align="left"><p>APC_LEVEL</p></td>
<td align="left"><p>任意</p></td>
</tr>
<tr class="even">
<td align="left"><p>LockControl</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>Nonarbitrary</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PnP</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>任意</p></td>
</tr>
<tr class="even">
<td align="left"><p>QueryEa</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>Nonarbitrary</p></td>
</tr>
<tr class="odd">
<td align="left"><p>QueryInformation</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>Nonarbitrary</p></td>
</tr>
<tr class="even">
<td align="left"><p>QueryQuota</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>Nonarbitrary</p></td>
</tr>
<tr class="odd">
<td align="left"><p>QuerySecurity</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>Nonarbitrary</p></td>
</tr>
<tr class="even">
<td align="left"><p>QueryVolumeInfo</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>Nonarbitrary</p></td>
</tr>
<tr class="odd">
<td align="left"><p>読み取り (I/O のページング) を除く</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>Nonarbitrary</p></td>
</tr>
<tr class="even">
<td align="left"><p>読み取り (ページング I/O パス)</p></td>
<td align="left"><p>APC_LEVEL</p></td>
<td align="left"><p>任意</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SetEa</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>Nonarbitrary</p></td>
</tr>
<tr class="even">
<td align="left"><p>SetInformation</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>Nonarbitrary</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SetQuota</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>Nonarbitrary</p></td>
</tr>
<tr class="even">
<td align="left"><p>SetSecurity</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>Nonarbitrary</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SetVolumeInfo</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>Nonarbitrary</p></td>
</tr>
<tr class="even">
<td align="left"><p>シャットダウン</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>任意</p></td>
</tr>
<tr class="odd">
<td align="left"><p>書き込み (I/O のページング) を除く</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
<td align="left"><p>Nonarbitrary</p></td>
</tr>
<tr class="even">
<td align="left"><p>書き込み (ページング I/O パス)</p></td>
<td align="left"><p>APC_LEVEL</p></td>
<td align="left"><p>任意</p></td>
</tr>
</tbody>
</table>

 

 

 




