---
title: インタロック キューのセットアップと使用
description: インタロック キューのセットアップと使用
ms.assetid: af44a4c0-5aa7-40aa-b511-df95c9bfe9bb
keywords:
- インタロック IRP キュー WDK カーネル
- 二重リンクされた Irp WDK カーネル
- ドライバー専用スレッドの WDK Irp
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7335fdbbd1d37fe9ef9878e1b8677ac46507616f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838425"
---
# <a name="setting-up-and-using-interlocked-queues"></a>インタロック キューのセットアップと使用





新しいドライバーでは、このセクションで説明する方法を優先して、[キャンセルセーフの IRP キュー](cancel-safe-irp-queues.md)フレームワークを使用する必要があります。

デバイス専用のスレッドを使用するドライバーまたは executive ワーカースレッド (ほとんどのシステム FSDs など) を使用するドライバーは、インタロックされたキュー内の Irp の独自のランタイム内部キューを管理するための最も可能性の高い種類のドライバーです。 また、WDM ドライバーを含むすべての PnP ドライバーは、PnP と電源状態の移行中に特定の Irp を内部にキューに入れなければなりません。

通常、これらのドライバーは、二重にリンクされたインタロックされたキューを設定します。各 IRP には、 [**LIST\_ENTRY**](https://docs.microsoft.com/windows/desktop/api/ntdef/ns-ntdef-_list_entry)型のメンバーが含まれています。このエントリは、ドライバーが現在保持している irp を二重にリンクするために使用できます。 単一のリンクされたインタロックされたキューを設定すると、ドライバーが Irp をキューへして再試行することはできません。

### <a href="" id="ddk-using-an-interlocked-queue-kg"></a>

ドライバーは、デバイスの初期化時に、インタロックされたキューを設定する必要があります。 次の図は、二重にリンクされたインタロックされたキュー、ドライバーがこのようなキューを設定するために呼び出す必要があるサポートルーチン、およびドライバーが Irp を挿入してキューから Irp を削除するために呼び出すことができる一連の**Exinterlocked ロック * Xxx*** ルーチンを示しています。

![インタロックキューの使用を示す図](images/3intlokq.png)

この図に示すように、ドライバーは、二重にリンクされたインタロックキューを設定するために、キュー自体と次のストレージを提供する必要があります。

-   Executive スピンロック。ドライバーは初期化のために[**keinitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializespinlock)を呼び出す必要があります。 通常、ドライバーは、 [*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンでデバイスオブジェクトのデバイス拡張機能を設定するときに、スピンロックを初期化します。

-   キューのリストの先頭。ドライバーは[**InitializeListHead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-initializelisthead)を呼び出すことによって初期化する必要があります。

ダブルリンクインタロックされたインタロックキューを使用するほとんどのドライバーは、ドライバーによって作成されたデバイスオブジェクトのデバイス拡張機能に必要な記憶域を提供します。 代わりに、コントローラー拡張機能 (ドライバーが[コントローラーオブジェクト](using-controller-objects.md)を使用している場合)、またはドライバーによって割り当てられた非ページプールで、キューおよび executive スピンロックを使用できます。

ドライバーは i/o 要求を受け入れていますが、次のいずれかのサポートルーチンを呼び出すことによって、IRP をキューに挿入することができます。これには、前の図に示すように、 *ListHead*の型が**LIST\_ENTRY**である必要があります。

[**ExInterlockedInsertTailList**](https://msdn.microsoft.com/library/windows/hardware/ff545402)は、IRP をキューの末尾に配置します。

[**ExInterlockedInsertHeadList**](https://msdn.microsoft.com/library/windows/hardware/ff545397)は、IRP をキューの先頭に配置します。 通常、ドライバーは、特定の要求を再試行する必要がある場合にのみ、このルーチンを呼び出します。

ドライバーは、これらの各**ExInterlockedInsert*Xxx*リスト**ルーチンに対して、以前に初期化された*ListHead*および executive スピンロック (*ロック*) ポインターに加えて、IRP (*ListEntry*) へのポインターを渡す必要があります。 [**ExInterlockedRemoveHeadList**](https://msdn.microsoft.com/library/windows/hardware/ff545427)を呼び出すことによってドライバーが IRP をデキュー場合は、 *ListHead*と*Lock*へのポインターのみが必要です。 デッドロックを防ぐために、ドライバーは、任意の**Exinterlocked ロック * Xxx*** ルーチンに渡す、execuに適合する inlock を保持しないようにする必要があります。

インタロックされたキューは executive スピンロックによって保護されているため、ドライバーは Irp をダブルリンクされたキューに挿入し、IRQL = ディスパッチ\_レベル以下で実行されている任意のドライバールーチンから、マルチプロセッサセーフな方法で Irp を削除できます。

前の図に示したように、 **list\_ENTRY**型の ListHead を持つキューは、ダブルリンクリストです。 ListHead という[ **\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)型のを持つ1つは、シーケンス処理された単一のリンクリストです。 ドライバーは、 [**ExInitializeSListHead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-initializeslisthead)を呼び出すことによって、シーケンスされた単一の連結されたインタロックキューの ListHead を初期化します。

I/o 操作を再試行しないドライバーでは、 [**ExInterlockedPushEntrySList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinterlockedpushentryslist)と[**ExInterlockedPopEntrySList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinterlockedpopentryslist)を使用して、シーケンス処理された単一リンクのインタロックされたキューで内部的に irp のキューを管理できます。 この種類のインタロックされたキューを使用するすべてのドライバーは、[前の図](#ddk-using-an-interlocked-queue-kg)に示すように、ListHead ヘッダー型および Execu対応の inlock **\_** 型ののための常駐ストレージも提供する必要があります。 **ExInterlockedPushEntrySList**を呼び出して最初のエントリをキューに挿入する前に、スピンロックを初期化し、そのキューを設定する必要があります。

詳細については、「[ハードウェアの優先順位](managing-hardware-priorities.md)と[スピンロック](spin-locks.md)の管理」を参照してください。 特定のサポートルーチンの IRQL 要件については、ルーチンのリファレンスページを参照してください。

 

 




