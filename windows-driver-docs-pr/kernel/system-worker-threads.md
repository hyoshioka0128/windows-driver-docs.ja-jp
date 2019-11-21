---
title: システム ワーカー スレッド
description: システム ワーカー スレッド
ms.assetid: 01ae1c1b-0cb0-4b9b-bd74-341b7c289fd4
keywords:
- executive ワーカースレッドの WDK カーネル
- 作業項目 WDK カーネル
- スレッドオブジェクト WDK カーネル
- 作業項目
- WorkItemEx
- ワーカースレッドの WDK カーネル
- ワーカースレッドコールバックルーチン WDK カーネル
- コールバックルーチン WDK ワーカースレッド
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: df678188abc431fe7ce9de7aa567173c9bff41b5
ms.sourcegitcommit: 46853426563bfac36651565181d7edac339f63af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74261433"
---
# <a name="system-worker-threads"></a>システム ワーカー スレッド





遅延処理を必要とするドライバーは、実際の処理を実行するドライバーコールバックルーチンへのポインターを含む*作業項目*を使用できます。 このドライバーは作業項目をキューに置いて、*システムワーカースレッド*がキューから作業項目を削除し、ドライバーのコールバックルーチンを実行します。 システムは、これらのシステムワーカースレッドのプールを保持します。これらのスレッドはそれぞれ、一度に1つの作業項目を処理するシステムスレッドです。

このドライバー[*は、作業項目のコールバック*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_workitem_routine)ルーチンを作業項目に関連付けます。 システムワーカースレッドは、作業項目を処理するときに、関連付けられている*WorkItem*ルーチンを呼び出します。 Windows Vista 以降のバージョンの Windows では、代わりに、ドライバーが[*Workitemex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_workitem_routine_ex)ルーチンを作業項目に関連付けることができます。 *Workitemex*は、 *WorkItem*によって実行されるパラメーターとは異なるパラメーターを受け取ります。

*WorkItem*ルーチンと*workitemex*ルーチンは、システムスレッドコンテキストで実行されます。 ドライバーディスパッチルーチンをユーザーモードのスレッドコンテキストで実行できる場合、そのルーチンは、作業*項目*または*workitemex*ルーチンを呼び出して、システムスレッドコンテキストを必要とする操作を実行できます。

作業項目を使用するために、ドライバーは次の手順を実行します。

1.  新しい作業項目を割り当てて初期化します。

    システムは、作業項目を保持するために、 [**IO\_WORKITEM**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)構造体を使用します。 新しい**IO\_workitem**構造体を割り当て、それを作業項目として初期化するには、ドライバーは[**Ioallocateworkitem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateworkitem)を呼び出すことができます。 Windows Vista 以降のバージョンの Windows では、ドライバーによって独自の**IO\_** 作業項目構造を割り当てることができます。また、 [**ioinitializeworkitem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinitializeworkitem)を呼び出して、構造体を作業項目として初期化します。 (ドライバーは、作業項目を保持するために必要なバイト数を判断するために、 [**IoSizeofWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosizeofworkitem)を呼び出す必要があります)。

2.  コールバックルーチンを作業項目に関連付けて、システムワーカースレッドによって処理されるように作業項目をキューに配置します。

    作業*項目ルーチンを*作業項目に関連付け、作業項目をキューに置いた場合、ドライバーは[**ioqueueworkitem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioqueueworkitem)を呼び出す必要があります。 代わりに、 *workitemex*ルーチンを作業項目に関連付け、作業項目をキューに置いて、ドライバーは[**Ioqueueworkitemex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioqueueworkitemex)を呼び出す必要があります。

3.  作業項目が不要になったら、それを解放します。

    **Ioallocateworkitem**によって割り当てられた作業項目は、 [**IoFreeWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeworkitem)によって解放される必要があります。 **Ioinitializeworkitem**によって初期化された作業項目は、解放する前に、 [**iouninitializeworkitem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iouninitializeworkitem)で初期化されていない必要があります。

    作業項目が現在キューに登録されていない場合にのみ、作業項目を初期化または解放できます。 システムは、作業項目のコールバックルーチンを呼び出す前に作業項目をデキューします。そのため、 **IoFreeWorkItem**と**Iouninitializeworkitem**は、コールバック内から呼び出すことができます。

時間のかかる処理を必要とする処理タスクを開始する必要がある DPC、またはブロック呼び出しを行う必要がある場合は、そのタスクの処理を1つ以上の作業項目に委任する必要があります。 DPC の実行中は、すべてのスレッドの実行が妨げられます。 また、IRQL = ディスパッチ\_レベルで実行される DPC は、ブロック呼び出しを行うことはできません。 ただし、作業項目を処理するシステムワーカースレッドは、IRQL = パッシブ\_レベルで実行されます。 このため、作業項目にブロック呼び出しを含めることができます。 たとえば、システムワーカースレッドは、ディスパッチャーオブジェクトを待機できます。

システムワーカースレッドのプールは限られたリソースなので、 *WorkItem*と*workitemex*ルーチンは、短時間で実行される操作に対してのみ使用できます。 これらのルーチンの1つが長時間実行されている (たとえば、無限ループが含まれている) 場合や、長時間待機している場合は、システムでデッドロックが発生する可能性があります。 そのため、ドライバーが遅延処理の長い時間を必要とする場合は、代わりに[**PsCreateSystemThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pscreatesystemthread)を呼び出して、独自のシステムスレッドを作成する必要があります。

既にキューにある作業項目をキューに登録するには、 **Ioqueueworkitem**または**Ioqueueworkitemex**を呼び出さないでください。 これにより、システムデータ構造が破損する可能性があります。 ドライバーが特定のドライバールーチンを実行するたびに同じ作業項目をキューに登録している場合は、次の方法を使用して、既にキューにある場合に、作業項目が2回目にキューに登録されないようにすることができます。

-   このドライバーは、ワーカールーチンのタスクの一覧を保持します。
-   このタスク一覧は、ワーカールーチンに提供されているコンテキストで使用できます。 タスク一覧を変更するワーカールーチンとドライバールーチンは、そのアクセスをリストに同期します。
-   ワーカールーチンを実行するたびに、リスト内のすべてのタスクが実行され、タスクが完了すると、各タスクが一覧から削除されます。
-   新しいタスクが到着すると、ドライバーはこのタスクを一覧に追加します。 タスク一覧が以前に空だった場合にのみ、ドライバーは作業項目をキューに置いています。

システムワーカースレッドは、ワーカースレッドを呼び出す前に、キューから作業項目を削除します。 したがって、ワーカースレッドが実行を開始するとすぐに、ドライバースレッドで作業項目を安全にキューに戻すことができます。

 

 




