---
title: ファイル システム オブジェクトの I/O ルーチン
description: ファイル システム オブジェクトの I/O ルーチン
ms.assetid: 0514e396-76b9-458b-9a98-e539d7e90274
keywords:
- ミニ リダイレクター WDK、オブジェクトの入出力ルーチン
- I/O WDK ネットワーク リダイレクター
- 低い i/o ルーチン WDK ネットワーク リダイレクター
- ファイル システム オブジェクト I/O WDK
- ファイル オブジェクト WDK のミニ リダイレクター
- WDK のミニ リダイレクター オブジェクト
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 432abfc4b4636c2ad4f4cae1b26062e6218f03c5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383830"
---
# <a name="file-system-object-io-routines"></a>ファイル システム オブジェクトの I/O ルーチン


ファイル システム オブジェクト I/O ルーチンでは、従来のファイル I/O を読み取り、書き込み、およびその他のファイル操作の呼び出しを表します。 これらのルーチンは、ネットワークのミニ リダイレクターの「低い I/O ルーチン」を多くの場合、呼び出されます。 RDBSS が特定の IRP を受信したときにこれらのルーチンを呼び出す

低い I/O ルーチンは、日常的なポインターの配列としての MINIRDR の一部としてに渡されるで\_にディスパッチ構造体が渡される、 [ **RxRegisterMinirdr** ](https://msdn.microsoft.com/library/windows/hardware/ff554693)ネットワークに登録するために使用するルーチンスタートアップ時に、ミニリダイレクター (で、 **DriverEntry**ルーチン)。 配列エントリの値は、低の I/O 操作を実行します。

これらの低い I/O またはファイル システム オブジェクトの入出力ルーチンは通常によって非同期に呼び出さ RDBSS します。 ようにネットワーク ミニリダイレクターする必要がありますを特定、低い I/O ルーチン実装されていることができますが安全に非同期に呼び出されます。 非同期呼び出しの要求を無視し、同期的にのみ動作するルーチンを実装する、ネットワーク ミニ リダイレクターのこともできます。 ただし、(読み取りし、書き込みなど) は、完了するまで時間がかかる特定の呼び出し、これらの同期と操作を実装する大幅に短縮できます全体のオペレーティング システムの I/O パフォーマンス。

すべてのファイル システム オブジェクト I/O ルーチンは、RX へのポインターを期待\_をパラメーターとして渡されるコンテキストの構造体。 RDBSS がのメンバーの数の値を設定するこれらのルーチンを呼び出す前に、 **LowIoContext** 、RX の構造\_コンテキスト。 一部のメンバーの**LowIoContext**一部のメンバーは特定のルーチンに対してのみ設定中に、すべてのルーチンでは、構造体が設定されます。 RX\_コンテキスト データ構造が処理されているが IRP が含まれています、 **LowIoContext.Operation**低の I/O 操作を実行するを指定するメンバー。 ネットワークのミニ リダイレクターで同じルーチンを指すため、低い I/O ルーチンのいくつかのことがこの**LowIoContext.Operation**メンバーは、要求された低い I/O 操作を区別するために使用することができます。 たとえば、ファイルのロックに関連するすべての I/O 呼び出しを使用するネットワーク ミニリダイレクターで同じ低い I/O ルーチンを呼び出すでした、 **LowIoContext.Operation**ロックを区別する、または要求された操作のロックを解除するメンバー。

その他のファイル I/O ルーチンが対象に、低い I/O ルーチンが同期呼び出しに基づくは以外の将来の変更のリリースの Windows オペレーティング システム。

LowIo パスの中に、 **LowIoContext.ResourceThreadId** 、RX のメンバー\_コンテキスト RDBSS で操作を開始した所有元のスレッドを示すことが保証されます。 **LowIoContext.ResourceThreadId**メンバーは、別のスレッドの代わりに FCB リソースを解放するために使用できます。 非同期のルーチンが完了したら、最初のスレッドから取得された FCB リソースを解放できます。

場合、 **MrxLowIoSubmit\[LOWIO\_OP\_XXX\]** ルーチンの完了に長時間かかる可能性がありますが、ネットワークのミニ リダイレクター ドライバーは、前に FCB リソースを解放する必要がありますネットワーク通信を開始しています。 FCB のリソースを呼び出すことによって解放できます[ **RxReleaseFcbResourceForThreadInMRx**](https://msdn.microsoft.com/library/windows/hardware/ff554694)します。

次の表では、ファイル システム オブジェクトの I/O (低い I/O) 操作のため、ネットワーク ミニ リダイレクターで実装できるルーチンを示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ルーチン</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550703" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_EXCLUSIVELOCK]&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550703)"><strong>MRxLowIOSubmit[LOWIO_OP_EXCLUSIVELOCK]</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターが、ファイル オブジェクトの排他ロックを開くことを要求するには、このルーチンを呼び出します。 RDBSS、IRP_MJ_LOCK_CONTROL IRP_MN_LOCK と IrpSp - マイナー コードを受信したときにこの呼び出しを発行する&gt;フラグは SL_EXCLUSIVE_LOCK ビットが設定されています。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550709" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_FSCTL]&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550709)"><strong>MRxLowIOSubmit[LOWIO_OP_FSCTL]</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターにファイル システムのコントロール要求を渡すには、このルーチンを呼び出します。 RDBSS では、受信、IRP_MJ_FILE_SYSTEM_CONTROL への応答には、この呼び出しを発行します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550715" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_IOCTL]&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550715)"><strong>MRxLowIOSubmit[LOWIO_OP_IOCTL]</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターに I/O システムのコントロール要求を渡すには、このルーチンを呼び出します。 RDBSS では、受信、IRP_MJ_DEVICE_CONTROL または IRP_MJ_INTERNAL_DEVICE_CONTROL への応答には、この呼び出しを発行.</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550721" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_NOTIFY_CHANGE_DIRECTORY]&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550721)"><strong>MRxLowIOSubmit[LOWIO_OP_NOTIFY_CHANGE_DIRECTORY]</strong></a></td>
<td align="left"><p>RDBSS は、ディレクトリ変更通知操作のネットワークのミニ リダイレクターに要求を発行するには、このルーチンを呼び出します。 RDBSS では、受信、IRP_MJ_DIRECTORY_CONTROL への応答には、この呼び出しを発行します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550724" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_READ]&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550724)"><strong>MRxLowIOSubmit[LOWIO_OP_READ]</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターに読み取り要求を発行するには、このルーチンを呼び出します。 RDBSS では、受信、IRP_MJ_READ への応答には、この呼び出しを発行します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550734" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_SHAREDLOCK]&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550734)"><strong>MRxLowIOSubmit[LOWIO_OP_SHAREDLOCK]</strong></a></td>
<td align="left"><p>RDBSS は、ネットワーク リダイレクターが、ファイル オブジェクトの共有ロックを開くことを要求するには、このルーチンを呼び出します。 RDBSS、IRP_MJ_LOCK_CONTROL IRP_MN_LOCK と IrpSp - マイナー コードを受信したときにこの呼び出しを発行する&gt;フラグのビット SL_EXCLUSIVE_LOCK セットはありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550740" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_UNLOCK]&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550740)"><strong>MRxLowIOSubmit[LOWIO_OP_UNLOCK]</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターが 1 つのファイル オブジェクトのロックを削除することを要求するには、このルーチンを呼び出します。 RDBSS、IRP_MJ_LOCK_CONTROL IRP_MN_UNLOCK_SINGLE の小さなコードを受信したときにこの呼び出しを発行します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550745" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_UNLOCK_MULTIPLE]&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550745)"><strong>MRxLowIOSubmit[LOWIO_OP_UNLOCK_MULTIPLE]</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターが、ファイル オブジェクトに保持されている複数のロックを削除することを要求するには、このルーチンを呼び出します。 RDBSS、IRP_MJ_LOCK_CONTROL IRP_MN_UNLOCK_ALL または IRP_MN_UNLOCK_ALL_BY_KEY の小さなコードを受信したときにこの呼び出しを発行します。 バイト範囲は、ロックを解除するがで指定された、 <strong>LowIoContext.ParamsFor.Locks.LockList</strong> RX_CONTEXT のメンバー。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550746" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_WRITE]&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550746)"><strong>MRxLowIOSubmit[LOWIO_OP_WRITE]</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターに書き込み要求を発行するには、このルーチンを呼び出します。 RDBSS では、受信、IRP_MJ_WRITE への応答には、この呼び出しを発行します。</p></td>
</tr>
</tbody>
</table>

 

 

 




