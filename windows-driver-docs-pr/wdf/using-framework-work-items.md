---
title: フレームワーク作業項目の使用
description: フレームワーク作業項目の使用
ms.assetid: d7e6d187-bed4-4071-a50b-90f32c4f0d5a
keywords:
- 作業項目 WDK KMDF
- キュー WDK KMDF、フレームワーク作業項目
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0cb0ebea7d4dd3bc2afeb064c3058aa9c1a130f5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843080"
---
# <a name="using-framework-work-items"></a>フレームワーク作業項目の使用





*作業項目*は、ドライバーが[*evtworkitem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem)イベントコールバック関数で実行するタスクです。 これらの関数は、システムワーカースレッドのコンテキストで、IRQL = パッシブ\_レベルで非同期的に実行されます。

フレームワークベースのドライバーは、通常、IRQL = ディスパッチ\_レベルで実行される[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)関数または[*EvtDpcFunc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdpc/nc-wdfdpc-evt_wdf_dpc)関数が、IRQL = パッシブ\_レベルで追加の処理を実行する必要がある場合に、作業項目を使用します。

つまり、IRQL = ディスパッチ\_レベルで実行される関数が、IRQL = パッシブ\_レベルでのみ呼び出すことができる関数を呼び出す必要がある場合、ドライバーは作業項目を使用できます。

通常、ドライバーの[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)または[*EvtDpcFunc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdpc/nc-wdfdpc-evt_wdf_dpc) callback 関数は、作業項目オブジェクトを作成し、それをシステムの作業項目キューに追加します。 その後、システムワーカースレッドによってオブジェクトがデキューされ、作業項目の[*Evtworkitem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem)コールバック関数が呼び出されます。

### <a name="sample-drivers-that-use-work-items"></a>作業項目を使用するサンプルドライバー

作業項目を使用する[サンプルフレームワークベースのドライバー](sample-kmdf-drivers.md)には、1394、AMCC5933、PCIDRV、およびトースターがあります。

### <a href="" id="ddk-setting-up-a-work-item-df"></a>作業項目の設定

作業項目を設定するには、次の操作を行う必要があります。

1.  作業項目を作成します。

    ドライバーは、 [**Wdfworkitemcreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemcreate)を呼び出して、作業項目オブジェクトを作成し、作業項目を処理する[*evtworkitem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem)コールバック関数を識別します。

2.  作業項目に関する情報を格納します。

    通常、ドライバーは、作業項目オブジェクトのコンテキストメモリを使用して、 [*Evtworkitem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem)コールバック関数が実行するタスクに関する情報を格納します。 *Evtworkitem*コールバック関数が呼び出されると、このコンテキストメモリにアクセスして情報を取得できます。 コンテキストメモリを割り当ててアクセスする方法の詳細については、「[フレームワークオブジェクトコンテキスト空間](framework-object-context-space.md)」を参照してください。

3.  作業項目をシステムの作業項目キューに追加します。

    ドライバーは、 [**Wdfworkitemenqueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemenqueue)キューを呼び出します。これにより、ドライバーの作業項目が作業項目キューに追加されます。

ドライバーが[**Wdfworkitemcreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemcreate)を呼び出す場合は、フレームワークデバイスオブジェクトまたはフレームワークキューオブジェクトへのハンドルを指定する必要があります。 そのオブジェクトを削除すると、そのオブジェクトに関連付けられている既存の作業項目もすべて削除されます。 作業項目オブジェクトは破棄され、関連付けられている作業項目のコールバックは、親オブジェクトの[*Evtcleanupcallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup)コールバックが呼び出される前にクリーンアップされます。

フレームワークオブジェクト階層のクリーンアップ規則の詳細については、「[フレームワークオブジェクトのライフサイクル](https://docs.microsoft.com/windows-hardware/drivers/wdf/framework-object-life-cycle)」を参照してください。

### <a href="" id="ddk-using-the-work-item-callback-function-df"></a>作業項目のコールバック関数の使用

作業項目キューに追加された作業項目は、システムワーカースレッドが使用可能になるまでキューに残ります。 システムワーカースレッドは、キューから作業項目を削除した後、ドライバーの[*Evtworkitem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem)コールバック関数を呼び出して、作業項目オブジェクトを入力として渡します。

通常、 [*Evtworkitem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem)コールバック関数は、次の手順を実行します。

1.  作業項目オブジェクトのコンテキストメモリにアクセスすることによって、作業項目に関するドライバーから提供される情報を取得します。

2.  指定したタスクを実行します。 必要に応じて、コールバック関数は[**WdfWorkItemGetParentObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemgetparentobject)を呼び出して、作業項目の親オブジェクトを決定できます。

3.  [**Wdfobjectdelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)を呼び出して作業項目オブジェクトを削除します。または、ドライバーが作業項目をキューへする場合は、作業項目へのハンドルを再利用できるようになったことを示します。

各作業項目のコールバック関数が実行するタスクは、比較的短い必要があります。 オペレーティングシステムは、限られた数のシステムワーカースレッドを提供します。そのため、時間のかかるタスクを実行するために作業項目のコールバック関数を使用する場合、ドライバーはシステムのパフォーマンスを阻害する可能性があります。

### <a href="" id="ddk-creating-and-deleting-work-items-df"></a>作業項目の作成と削除

ドライバーは、次の2つの方法のいずれかを使用して、作業項目を作成および削除できます。

-   各作業項目を1回だけ使用します。必要に応じて作業項目を作成し、使用後すぐに削除します。

    この手法は、少数の作業項目に対して頻繁に使用しない (1 分間に1回未満) 必要があるドライバーに役立ちます。

    たとえば、ドライバーの[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)コールバック関数は、 [**Wdfworkitemcreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemcreate)を呼び出してから、 [**wdfworkitemcreate キュー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemenqueue)を呼び出すことができます。また、作業項目の[*Evtworkitem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem)コールバック関数は、 [**wdfworkitemcreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)を呼び出すことができます。

    ドライバーがこのシナリオに従っていて、 [*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc) callback 関数が、 [**Wdfworkitemcreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemcreate)から返される値\_\_リソースが不足している場合、ドライバーは必要な作業を延期できる必要があります。システムリソース (通常はメモリ) が使用可能になります。

-   必要に応じて、ドライバーがキューする1つ以上の作業項目を作成します。

    この手法は、作業項目を頻繁に使用するドライバー (1 分に1回以上) を使用する場合や、ドライバーの[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)コールバック関数が\_状態を簡単に処理できない場合に便利です\_リソースから[**値が返されます。WdfWorkItemCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemcreate)。

    システムは、ドライバーが[**Wdfworkitemenqueue キュー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemenqueue)を呼び出すまで、作業項目にワーカースレッドを割り当てません。 したがって、システムワーカースレッドはリソースが限られていますが、デバイスの初期化中に作業項目を作成すると、少量のメモリを消費しますが、それ以外の場合はシステムのパフォーマンスに影響しません。

    次の手順では、考えられるシナリオについて説明します。

    1.  ドライバーの[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数は、 [**Wdfworkitemcreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemcreate)を呼び出して、作業項目ハンドルを取得します。
    2.  ドライバーの[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc) callback 関数は、手順 1. のハンドルを使用して、 [*evtworkitem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem)コールバック関数が実行する必要があるアクションのリストを作成し、 [**wdfworkitemenqueue キュー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemenqueue)を呼び出します。
    3.  ドライバーの[*Evtworkitem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem)コールバック関数は、アクションの一覧を実行し、コールバック関数が実行されたことを示すフラグを設定します。

    その後、ドライバーの[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc) callback 関数が呼び出されるたびに、 [*evtworkitem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem)コールバック関数が実行されたかどうかを判断する必要があります。 *Evtworkitem*コールバック関数が実行されていない場合、作業項目がまだキューに登録されているため、 *EvtInterruptDpc* Callback 関数は[**wdfworkitemenqueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemenqueue)を呼び出しません。 この場合、 *EvtInterruptDpc* callback 関数は、 *evtworkitem*コールバック関数のアクションの一覧のみを更新します。

    各作業項目は、デバイスまたはキューに関連付けられています。 関連付けられているデバイスまたはキューが削除されると、フレームワークは、関連付けられているすべての作業項目を削除します。この手法を使用する場合、ドライバーは[**Wdfobjectdelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)を呼び出す必要がありません。

いくつかのドライバーでは、作業項目キューから作業項目をフラッシュするために、 [**Wdfworkitemflush**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemflush)を呼び出す必要がある場合があります。 **Wdfworkitemflush**の使用例については、メソッドのリファレンスページを参照してください。

ドライバーが未処理の作業項目に対して[**Wdfobjectdelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)を呼び出す場合、結果は作業項目の状態によって異なります。

|作業項目の状態|結果|
|-|-|
|作成済みでエンキューされていない|作業項目はすぐにクリーンアップされます。|
|入っ|[**Wdfobjectdelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)の呼び出しは、作業項目の実行が完了するまで待機してから、作業項目がクリーンアップされます|
|実行|ドライバーが[*Evtworkitem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem) (同じスレッド) 内から[**wdfobjectdelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)を呼び出すと、 [**wdfobjectdelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)は直ちに返されます。 [*Evtworkitem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem)が完了すると、作業項目がクリーンアップされます。  それ以外の場合、 [**Wdfobjectdelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)は EvtWorkItem が終了するまで待機します。|

 





