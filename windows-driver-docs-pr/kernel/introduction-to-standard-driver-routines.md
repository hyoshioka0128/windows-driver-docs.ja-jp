---
title: 標準ドライバー ルーチンの概要
description: 標準ドライバー ルーチンの概要
ms.assetid: 91aaca02-a571-4058-b5af-98277fcbcf9d
keywords:
- 標準のドライバー ルーチンについて、標準のドライバー ルーチンの WDK カーネル
- 標準のドライバー ルーチンについて、ドライバー ルーチンの WDK カーネル
- ルーチン WDK カーネルでは、標準のドライバー ルーチンについて
- Irp WDK カーネルでは、標準のドライバーのルーチン
- 必須の標準的なルーチンの WDK カーネル
- 省略可能な標準ルーチン WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d6aa9f5c98ea0cce6ddb7c302569f63a2e957eb
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350349"
---
# <a name="introduction-to-standard-driver-routines"></a>標準ドライバー ルーチンの概要





システム定義の標準のドライバーのルーチンのセットは各カーネル モード ドライバー構築します。 カーネル モード ドライバー プロセス*I/O 要求パケット*(Irp) システムによって提供されるドライバー サポート ルーチンを呼び出すことによってこれらの標準的なルーチン内で。

すべてのドライバーのアタッチされたドライバーは、チェーン内のレベルに関係なく必要があります基本的な一連の標準的なルーチン Irp を処理するためにします。 ドライバーが追加の標準的なルーチンを実装する必要があるかどうかは、ドライバーの物理デバイスを制御または物理デバイス ドライバー、および基になる物理デバイスの性質上に構築されたかどうかによって異なります。 物理デバイスを制御する最下位レベルのドライバーより高度なドライバーは、通常 Irp を処理するための下位のドライバーに渡すよりもより必要なルーチンがあります。

標準のドライバーのルーチンは、2 つのグループに分割できます。 各カーネル モード ドライバーを持つ必要があります、およびドライバーの種類と場所に応じて、省略可能なもの、*デバイス スタック*。

このセクションでは、必須の標準的な手順について説明します。 その他のセクションでは、省略可能なルーチンについて説明します。

2 つのテーブルを次に示します。 最初のテーブルには、必須の標準的な手順が一覧表示します。 2 つ目は、省略可能なルーチンのほとんどを一覧表示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>標準のドライバーのルーチンが必要</th>
<th>目的</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize">DriverEntry</a></strong></p></td>
<td><p>ドライバーとドライバー、そのオブジェクトを初期化します。</p></td>
<td><p><a href="writing-a-driverentry-routine.md" data-raw-source="[Writing a DriverEntry Routine](writing-a-driverentry-routine.md)">DriverEntry ルーチンを記述します。</a></p></td>
</tr>
<tr class="even">
<td><p><em><a href="https://msdn.microsoft.com/library/windows/hardware/ff540521">AddDevice</a></em></p></td>
<td><p>デバイスを初期化し、デバイス オブジェクトを作成します。</p></td>
<td><p><a href="writing-an-adddevice-routine.md" data-raw-source="[Writing an AddDevice Routine](writing-an-adddevice-routine.md)">AddDevice、ルーチンを記述します。</a></p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/dispatchcreate--dispatchclose--and-dispatchcreateclose-routines">ディスパッチ ルーチン</a></p></td>
<td><p>受信および Irp を処理します。</p></td>
<td><p><a href="writing-dispatch-routines.md" data-raw-source="[Writing Dispatch Routines](writing-dispatch-routines.md)">書き込みディスパッチ ルーチン</a></p></td>
</tr>
<tr class="even">
<td><p><em>アンロード</em></p></td>
<td><p>ドライバーによって取得されたシステム リソースを解放します。</p></td>
<td><p><a href="writing-an-unload-routine.md" data-raw-source="[Writing an Unload Routine](writing-an-unload-routine.md)">アンロードするルーチンを記述します。</a></p></td>
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
<th>省略可能な標準のドライバーのルーチン</th>
<th>目的</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>再初期化します。</em></p></td>
<td><p>場合、ドライバーの初期化が完了すると<strong>DriverEntry</strong>ことはできません。</p></td>
<td><p><a href="writing-a-reinitialize-routine.md" data-raw-source="[Writing a Reinitialize Routine](writing-a-reinitialize-routine.md)">再初期化ルーチンを記述します。</a></p></td>
</tr>
<tr class="even">
<td><p><em>StartIo</em></p></td>
<td><p>物理デバイスの I/O 操作を開始します。</p></td>
<td><p><a href="writing-a-startio-routine.md" data-raw-source="[Writing a StartIo Routine](writing-a-startio-routine.md)">StartIo ルーチンを記述します。</a></p></td>
</tr>
<tr class="odd">
<td><p>割り込みサービス ルーチン</p></td>
<td><p>中断時に、デバイスの状態を保存します。</p></td>
<td><p><a href="writing-an-isr.md" data-raw-source="[Writing an ISR](writing-an-isr.md)">Isr</a></p></td>
</tr>
<tr class="even">
<td><p>遅延プロシージャ呼び出し</p></td>
<td><p>ISR デバイスの状態を保存した後は、デバイスの割り込みの処理を完了します。</p></td>
<td><p><a href="dpc-objects-and-dpcs.md" data-raw-source="[DPC Objects and DPCs](dpc-objects-and-dpcs.md)">DPC オブジェクトと Dpc</a></p></td>
</tr>
<tr class="odd">
<td><p><em>SynchCritSection</em></p></td>
<td><p>ドライバーのデータへのアクセスを同期します。</p></td>
<td><p><a href="using-critical-sections.md" data-raw-source="[Using Critical Sections](using-critical-sections.md)">重要なセクションを使用します。</a></p></td>
</tr>
<tr class="even">
<td><p><em>AdapterControl</em></p></td>
<td><p>DMA 操作を開始します。</p></td>
<td><p><a href="adapter-objects-and-dma.md" data-raw-source="[Adapter Objects and DMA](adapter-objects-and-dma.md)">アダプター オブジェクトと DMA</a></p></td>
</tr>
<tr class="odd">
<td><p><em>IoCompletion</em></p></td>
<td><p>IRP のドライバーの処理を完了します。</p></td>
<td><p><a href="completing-irps.md" data-raw-source="[Completing IRPs](completing-irps.md)">Irp の完了</a></p></td>
</tr>
<tr class="even">
<td><p><em>Cancel</em></p></td>
<td><p>IRP のドライバーの処理をキャンセルします。</p></td>
<td><p><a href="canceling-irps.md" data-raw-source="[Canceling IRPs](canceling-irps.md)">Irp のキャンセル</a></p></td>
</tr>
<tr class="odd">
<td><p><em>CustomTimerDpc</em>、 <em>IoTimer</em></p></td>
<td><p>タイミングと、イベントを同期します。</p></td>
<td><p><a href="synchronization-techniques.md" data-raw-source="[Synchronization Techniques](synchronization-techniques.md)">同期方法</a></p></td>
</tr>
</tbody>
</table>

 

現在 IRP とターゲット デバイス オブジェクトは、標準的な多くのルーチンへの入力パラメーターが。 すべてのドライバーでは、一連の標準的なルーチンによって段階的に各 IRP を処理します。

システム指定のドライバーを除くすべての標準的なルーチンの名前にプレフィックスを識別する、特定のドライバーまたはデバイスに固有の付加規則により、 **DriverEntry**します。 たとえば、このドキュメントでは"DD"のように、[ドライバー オブジェクトの図](introduction-to-driver-objects.md#driver-object-illustration)します。 この規則に従うと、デバッグやドライバーを管理するやすくになります。

 

 




