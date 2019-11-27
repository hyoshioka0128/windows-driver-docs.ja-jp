---
title: ファイル システム オブジェクトの I/O ルーチン
description: ファイル システム オブジェクトの I/O ルーチン
ms.assetid: 0514e396-76b9-458b-9a98-e539d7e90274
keywords:
- ミニリダイレクター WDK、オブジェクト i/o ルーチン
- I/o WDK ネットワークリダイレクター
- 低 i/o ルーチン WDK ネットワークリダイレクター
- ファイルシステムオブジェクトの i/o WDK
- ファイルオブジェクト WDK ミニリダイレクター
- オブジェクト WDK ミニリダイレクター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b12b3097cc530eac0c50e8b5cb07d3a0a14dca7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841408"
---
# <a name="file-system-object-io-routines"></a>ファイル システム オブジェクトの I/O ルーチン


ファイルシステムオブジェクトの i/o ルーチンは、読み取り、書き込み、およびその他のファイル操作のための従来のファイル i/o 呼び出しを表します。 これらのルーチンは、ネットワークミニリダイレクターでは "低 i/o ルーチン" と呼ばれることがよくあります。 RDBSS は、特定の IRP の受信に応答してこれらのルーチンを呼び出します。

低 i/o ルーチンは、スタートアップ時にネットワークミニリダイレクターを登録するために使用される[**RxRegisterMinirdr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxregisterminirdr)ルーチンに渡される minirdr\_ディスパッチ構造の一部として、ルーチンポインターの配列として渡されます ( **driverentry**内)。ルーチン)。 配列エントリの値は、実行する低 i/o 操作です。

これらの低 i/o またはファイルシステムオブジェクトの i/o ルーチンは、通常、RDBSS によって非同期に呼び出されます。 そのため、ネットワークミニリダイレクターは、実装されている低 i/o ルーチンを安全に非同期的に呼び出すことができるようにする必要があります。 ネットワークミニリダイレクターは、非同期呼び出しの要求を無視し、同期的にのみ動作するルーチンを実装することもできます。 ただし、特定の呼び出しが完了するまでに時間がかかる場合 (読み取りと書き込みなど)、これらを同期操作として実装すると、オペレーティングシステム全体の i/o パフォーマンスが大幅に低下する可能性があります。

すべてのファイルシステムオブジェクト i/o ルーチンは、RX\_コンテキスト構造体へのポインターをパラメーターとして渡すことを想定しています。 これらのルーチンを呼び出す前に、RDBSS は RX\_コンテキストの**Lowiocontext**構造に含まれる多数のメンバーの値を設定します。 **Lowiocontext**構造の一部のメンバーはすべてのルーチンに対して設定されますが、一部のメンバーは特定のルーチンに対してのみ設定されます。 RX\_CONTEXT データ構造体には、処理中の IRP が含まれており、実行する i/o 操作の下限を指定する**Lowiocontext 操作**メンバーが含まれています。 低 i/o ルーチンのいくつかは、ネットワークミニリダイレクターで同じルーチンを指すことができます。これは、この**Lowiocontext 操作**のメンバーが、要求された低 i/o 操作を区別するために使用できるためです。 たとえば、ファイルロックに関連するすべての i/o 呼び出しで、ネットワークミニリダイレクターで同じ低 i/o ルーチンを呼び出すことができます。これは、要求されたロック操作またはロック解除操作を区別するために、 **Lowiocontext. Operation**メンバーを使用します。

低 i/o ルーチン以外の他のファイル i/o ルーチンは、同期呼び出しに基づいていますが、これは Windows オペレーティングシステムの将来のリリースで変更される可能性があります。

LowIo パスでは、RX\_コンテキストの**Lowiocontext threadid**メンバーは、RDBSS で操作を開始した所有スレッドを示すことが保証されます。 **Lowiocontext threadid**メンバーを使用すると、別のスレッドに代わって FCB リソースを解放できます。 非同期ルーチンが完了すると、初期スレッドから取得された FCB リソースが解放されます。

**MrxLowIoSubmit\[LOWIO\_OP\_XXX\]** ルーチンの完了に時間がかかる可能性が高い場合、ネットワークミニリダイレクタードライバーは、ネットワーク通信を開始する前に、FCB リソースを解放する必要があります。 FCB リソースは、 [**RxReleaseFcbResourceForThreadInMRx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxreleasefcbresourceforthreadinmrx)を呼び出すことによって解放できます。

次の表に、ファイルシステムオブジェクト i/o (低 i/o) 操作のためにネットワークミニリダイレクターで実装できるルーチンを示します。

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
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-exclusivelock-" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_EXCLUSIVELOCK]&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-exclusivelock-)"><strong>MRxLowIOSubmit [LOWIO_OP_EXCLUSIVELOCK]</strong></a></td>
<td align="left"><p>RDBSS は、このルーチンを呼び出して、ネットワークミニリダイレクターがファイルオブジェクトの排他ロックを開くように要求します。 RDBSS は、マイナーコード IRP_MN_LOCK と IrpSp-&gt;フラグに SL_EXCLUSIVE_LOCK ビットが設定されている IRP_MJ_LOCK_CONTROL の受信に応答して、この呼び出しを発行します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-fsctl-" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_FSCTL]&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-fsctl-)"><strong>MRxLowIOSubmit [LOWIO_OP_FSCTL]</strong></a></td>
<td align="left"><p>RDBSS は、このルーチンを呼び出して、ファイルシステムコントロール要求をネットワークミニリダイレクターに渡します。 RDBSS は、IRP_MJ_FILE_SYSTEM_CONTROL の受信に応答してこの呼び出しを発行します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-ioctl-" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_IOCTL]&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-ioctl-)"><strong>MRxLowIOSubmit [LOWIO_OP_IOCTL]</strong></a></td>
<td align="left"><p>RDBSS はこのルーチンを呼び出して、ネットワークミニリダイレクターに i/o システム制御要求を渡します。 RDBSS は、IRP_MJ_DEVICE_CONTROL または IRP_MJ_INTERNAL_DEVICE_CONTROL の受信に応答して、この呼び出しを発行します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-notify-change-directory-" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_NOTIFY_CHANGE_DIRECTORY]&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-notify-change-directory-)"><strong>MRxLowIOSubmit [LOWIO_OP_NOTIFY_CHANGE_DIRECTORY]</strong></a></td>
<td align="left"><p>RDBSS は、このルーチンを呼び出して、ディレクトリ変更通知操作のためにネットワークミニリダイレクターに要求を発行します。 RDBSS は、IRP_MJ_DIRECTORY_CONTROL の受信に応答してこの呼び出しを発行します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-read-" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_READ]&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-read-)"><strong>MRxLowIOSubmit [LOWIO_OP_READ]</strong></a></td>
<td align="left"><p>RDBSS は、このルーチンを呼び出して、ネットワークミニリダイレクターに読み取り要求を発行します。 RDBSS は、IRP_MJ_READ の受信に応答してこの呼び出しを発行します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-sharedlock-" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_SHAREDLOCK]&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-sharedlock-)"><strong>MRxLowIOSubmit [LOWIO_OP_SHAREDLOCK]</strong></a></td>
<td align="left"><p>RDBSS は、このルーチンを呼び出して、ネットワークリダイレクターがファイルオブジェクトに対して共有ロックを開くことを要求します。 RDBSS は、マイナーコード IRP_MN_LOCK と IrpSp-&gt;フラグに SL_EXCLUSIVE_LOCK ビットが設定されていない IRP_MJ_LOCK_CONTROL を受信する応答として、この呼び出しを発行します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-unlock-" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_UNLOCK]&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-unlock-)"><strong>MRxLowIOSubmit [LOWIO_OP_UNLOCK]</strong></a></td>
<td align="left"><p>RDBSS は、このルーチンを呼び出して、ネットワークミニリダイレクターがファイルオブジェクトの1つのロックを解除するように要求します。 RDBSS は、IRP_MN_UNLOCK_SINGLE のマイナーコードを使用して IRP_MJ_LOCK_CONTROL を受け取ることに応答して、この呼び出しを発行します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-unlock-multiple-" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_UNLOCK_MULTIPLE]&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-unlock-multiple-)"><strong>MRxLowIOSubmit [LOWIO_OP_UNLOCK_MULTIPLE]</strong></a></td>
<td align="left"><p>RDBSS は、このルーチンを呼び出して、ファイルオブジェクトに保持されている複数のロックがネットワークミニリダイレクターによって削除されるように要求します。 RDBSS は、IRP_MN_UNLOCK_ALL または IRP_MN_UNLOCK_ALL_BY_KEY のマイナーコードを使用して IRP_MJ_LOCK_CONTROL を受け取ることに応答して、この呼び出しを発行します。 ロックを解除するバイト範囲は、RX_CONTEXT の<strong>Lowiocontext</strong>に指定されています。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-write-" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_WRITE]&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-write-)"><strong>MRxLowIOSubmit [LOWIO_OP_WRITE]</strong></a></td>
<td align="left"><p>RDBSS はこのルーチンを呼び出して、ネットワークミニリダイレクターに書き込み要求を発行します。 RDBSS は、IRP_MJ_WRITE の受信に応答してこの呼び出しを発行します。</p></td>
</tr>
</tbody>
</table>

 

 

 




