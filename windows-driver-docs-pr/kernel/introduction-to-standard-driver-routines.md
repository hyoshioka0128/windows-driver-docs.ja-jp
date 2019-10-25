---
title: 標準ドライバー ルーチンの概要
description: 標準ドライバー ルーチンの概要
ms.assetid: 91aaca02-a571-4058-b5af-98277fcbcf9d
keywords:
- 標準ドライバールーチン WDK カーネル、標準ドライバールーチンについて
- ドライバールーチン WDK カーネル、標準ドライバールーチンについて
- ルーチン WDK カーネル、標準ドライバールーチンについて
- Irp WDK カーネル、標準ドライバールーチン
- 必須の標準ルーチン WDK カーネル
- オプションの標準ルーチン WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5072f3e8247a174cc4dd700f923cfd4be973e0ad
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828178"
---
# <a name="introduction-to-standard-driver-routines"></a>標準ドライバー ルーチンの概要





各カーネルモードドライバーは、一連のシステム定義の標準ドライバールーチンを中心に構築されています。 カーネルモードドライバーは、システムによって提供されるドライバーサポートルーチンを呼び出すことによって、これらの標準ルーチン内の*i/o 要求パケット*(irp) を処理します。

すべてのドライバーは、アタッチされたドライバーのチェーン内のレベルに関係なく、Irp を処理するために標準ルーチンの基本セットを備えている必要があります。 ドライバーが追加の標準ルーチンを実装する必要があるかどうかは、ドライバーが物理デバイスを制御しているか、物理デバイスドライバーを介して管理されているか、および基礎となる物理デバイスの性質によって異なります。 物理デバイスを制御する最下位レベルのドライバーには、上位レベルのドライバーよりも多くの必須ルーチンがあります。通常は、Irp を下位のドライバーに渡して処理します。

標準ドライバールーチンは、各カーネルモードドライバーが持つ必要がある2つのグループと、*デバイススタック*内のドライバーの種類と場所によってはオプションである2つのグループに分けることができます。

ここでは、必須の標準ルーチンについて説明します。 その他のセクションでは、省略可能なルーチンについて説明します。

2つのテーブルを次に示します。 最初の表には、必要な標準ルーチンが示されています。 2つ目は、オプションのルーチンのほとんどを示しています。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>必須の標準ドライバールーチン</th>
<th>目的</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize">DriverEntry</a></strong></p></td>
<td><p>ドライバーとそのドライバーオブジェクトを初期化します。</p></td>
<td><p><a href="writing-a-driverentry-routine.md" data-raw-source="[Writing a DriverEntry Routine](writing-a-driverentry-routine.md)">DriverEntry ルーチンを記述する</a></p></td>
</tr>
<tr class="even">
<td><p><em><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device">AddDevice</a></em></p></td>
<td><p>デバイスを初期化し、デバイスオブジェクトを作成します。</p></td>
<td><p><a href="writing-an-adddevice-routine.md" data-raw-source="[Writing an AddDevice Routine](writing-an-adddevice-routine.md)">AddDevice ルーチンを記述する</a></p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/dispatchcreate--dispatchclose--and-dispatchcreateclose-routines">ディスパッチルーチン</a></p></td>
<td><p>Irp を受信および処理します。</p></td>
<td><p><a href="writing-dispatch-routines.md" data-raw-source="[Writing Dispatch Routines](writing-dispatch-routines.md)">ディスパッチルーチンの記述</a></p></td>
</tr>
<tr class="even">
<td><p><em>取り除き</em></p></td>
<td><p>ドライバーによって取得されたシステムリソースを解放します。</p></td>
<td><p><a href="writing-an-unload-routine.md" data-raw-source="[Writing an Unload Routine](writing-an-unload-routine.md)">アンロードルーチンを記述する</a></p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>省略可能な標準ドライバールーチン</th>
<th>目的</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>初期化</em></p></td>
<td><p><strong>Driverentry</strong>ができない場合は、ドライバーの初期化を完了します。</p></td>
<td><p><a href="writing-a-reinitialize-routine.md" data-raw-source="[Writing a Reinitialize Routine](writing-a-reinitialize-routine.md)">再初期化ルーチンを記述する</a></p></td>
</tr>
<tr class="even">
<td><p><em>StartIo</em></p></td>
<td><p>物理デバイスで i/o 操作を開始します。</p></td>
<td><p><a href="writing-a-startio-routine.md" data-raw-source="[Writing a StartIo Routine](writing-a-startio-routine.md)">StartIo ルーチンを記述する</a></p></td>
</tr>
<tr class="odd">
<td><p>割り込みサービスルーチン</p></td>
<td><p>中断時にデバイスの状態を保存します。</p></td>
<td><p><a href="writing-an-isr.md" data-raw-source="[Writing an ISR](writing-an-isr.md)">ISR の作成</a></p></td>
</tr>
<tr class="even">
<td><p>遅延プロシージャ呼び出し</p></td>
<td><p>ISR がデバイスの状態を保存した後に、デバイスの割り込み処理を完了します。</p></td>
<td><p><a href="dpc-objects-and-dpcs.md" data-raw-source="[DPC Objects and DPCs](dpc-objects-and-dpcs.md)">DPC オブジェクトと Dpc</a></p></td>
</tr>
<tr class="odd">
<td><p><em>SynchCritSection</em></p></td>
<td><p>ドライバーデータへのアクセスを同期します。</p></td>
<td><p><a href="using-critical-sections.md" data-raw-source="[Using Critical Sections](using-critical-sections.md)">クリティカルセクションの使用</a></p></td>
</tr>
<tr class="even">
<td><p><em>AdapterControl</em></p></td>
<td><p>DMA 操作を開始します。</p></td>
<td><p><a href="adapter-objects-and-dma.md" data-raw-source="[Adapter Objects and DMA](adapter-objects-and-dma.md)">アダプターオブジェクトと DMA</a></p></td>
</tr>
<tr class="odd">
<td><p><em>IoCompletion</em></p></td>
<td><p>IRP のドライバーの処理を完了します。</p></td>
<td><p><a href="completing-irps.md" data-raw-source="[Completing IRPs](completing-irps.md)">Irp の完了</a></p></td>
</tr>
<tr class="even">
<td><p><em>サブスクリプションの</em></p></td>
<td><p>IRP のドライバー処理をキャンセルします。</p></td>
<td><p><a href="canceling-irps.md" data-raw-source="[Canceling IRPs](canceling-irps.md)">Irp の取り消し</a></p></td>
</tr>
<tr class="odd">
<td><p><em>Customtimerdpc</em>、 <em>iotimer</em></p></td>
<td><p>タイミングおよび同期イベント。</p></td>
<td><p><a href="synchronization-techniques.md" data-raw-source="[Synchronization Techniques](synchronization-techniques.md)">同期方法</a></p></td>
</tr>
</tbody>
</table>

 

現在の IRP とターゲットデバイスオブジェクトは、多くの標準ルーチンの入力パラメーターです。 すべてのドライバーは、一連の標準ルーチンを通じて各 IRP を段階的に処理します。

慣例により、システム提供のドライバーは、ドライバー固有またはデバイス固有のプレフィックスを、 **Driverentry**以外のすべての標準ルーチンの名前に付加します。 例として、このドキュメントでは、[ドライバーオブジェクトの図](introduction-to-driver-objects.md#driver-object-illustration)に示すように、"DD" を使用しています。 この規則に従うことで、ドライバーのデバッグと管理が簡単になります。

 

 




