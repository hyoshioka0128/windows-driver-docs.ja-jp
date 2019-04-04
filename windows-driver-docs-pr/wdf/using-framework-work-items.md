---
title: 作業項目のフレームワークの使用
description: 作業項目のフレームワークの使用
ms.assetid: d7e6d187-bed4-4071-a50b-90f32c4f0d5a
keywords:
- WDK KMDF の作業項目します。
- WDK KMDF、フレームワークの作業項目キュー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab60d2b4898e02bea4557196b228fd660854245f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556960"
---
# <a name="using-framework-work-items"></a>作業項目のフレームワークの使用





A*作業項目*でドライバーを実行するタスクは、 [ *EvtWorkItem* ](https://msdn.microsoft.com/library/windows/hardware/ff541859)イベント コールバック関数。 これらの関数を非同期的に実行 IRQL = パッシブ\_システム ワーカー スレッドのコンテキストでのレベル。

場合にフレームワーク ベースのドライバーが作業項目によく使用して、 [ *EvtInterruptDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff541721)または[ *EvtDpcFunc* ](https://msdn.microsoft.com/library/windows/hardware/ff541683) IRQL で実行される関数を =ディスパッチ\_レベルでは、IRQL で追加の処理を実行する必要があります = パッシブ\_レベル。

つまり、ドライバーを作業項目を使用場合 IRQL で実行する関数をディスパッチ =\_レベルは、IRQL でのみ呼び出すことができる関数を呼び出す必要があります = パッシブ\_レベル。

通常、ドライバーの[ *EvtInterruptDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff541721)または[ *EvtDpcFunc* ](https://msdn.microsoft.com/library/windows/hardware/ff541683)コールバック関数が作業項目オブジェクトを作成し、それを追加しますシステムの作業項目キュー。 システム ワーカー スレッドがその後、オブジェクトをデキューし、呼び出し、作業項目の[ *EvtWorkItem* ](https://msdn.microsoft.com/library/windows/hardware/ff541859)コールバック関数。

### <a name="sample-drivers-that-use-work-items"></a>作業項目を使用しているサンプル ドライバー

[フレームワーク ベースのドライバーのサンプル](sample-kmdf-drivers.md)1394、AMCC5933、PCIDRV、およびトースターが作業項目使用してにはが含まれています。

### <a href="" id="ddk-setting-up-a-work-item-df"></a>作業項目の設定

作業項目を設定するには、ドライバーが必要です。

1.  作業項目を作成します。

    ドライバーの呼び出し[ **WdfWorkItemCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff551201)作業項目オブジェクトを作成して、識別するために、 [ *EvtWorkItem* ](https://msdn.microsoft.com/library/windows/hardware/ff541859)コールバック関数作業項目を処理します。

2.  作業項目に関する情報を格納します。

    通常、ドライバーを使用して作業項目オブジェクトのコンテキストのメモリ タスクに関する情報を格納する、 [ *EvtWorkItem* ](https://msdn.microsoft.com/library/windows/hardware/ff541859)コールバック関数を実行する必要があります。 ときに、 *EvtWorkItem*コールバック関数が呼び出されると、このコンテキストのメモリにアクセスして、情報を取得できます。 割り当てるし、コンテキストのメモリにアクセスする方法については、[フレームワーク オブジェクト コンテキストの空間](framework-object-context-space.md)を参照してください。

3.  システムの作業項目のキューに作業項目を追加します。

    ドライバーの呼び出し[ **WdfWorkItemEnqueue**](https://msdn.microsoft.com/library/windows/hardware/ff551203)、作業項目のキューに、ドライバーの作業項目を追加します。

ドライバーを呼び出すと[ **WdfWorkItemCreate**](https://msdn.microsoft.com/library/windows/hardware/ff551201)、framework デバイス オブジェクトまたはフレームワークのキュー オブジェクトのいずれかを識別するハンドルを指定する必要があります。 システムでは、そのオブジェクトを削除したときにも、オブジェクトに関連付けられている既存の作業項目を削除します。

### <a href="" id="ddk-using-the-work-item-callback-function-df"></a>作業項目のコールバック関数の使用

作業項目は、作業項目のキューに追加されたが、システムのワーカー スレッドが使用可能になるまで、キューに保持されます。 システム ワーカー スレッド、キューから作業項目を削除し、呼び出してドライバーの[ *EvtWorkItem* ](https://msdn.microsoft.com/library/windows/hardware/ff541859)コールバック関数を作業項目オブジェクトの入力として渡します。

通常、 [ *EvtWorkItem* ](https://msdn.microsoft.com/library/windows/hardware/ff541859)コールバック関数は、次の手順を実行します。

1.  作業項目オブジェクトのコンテキストのメモリにアクセスすることには、作業項目に関するドライバーによって提供される情報を取得します。

2.  指定したタスクを実行します。 かどうか、必要に応じて、コールバック関数は、呼び出して[ **WdfWorkItemGetParentObject** ](https://msdn.microsoft.com/library/windows/hardware/ff551207)作業項目の親オブジェクトを決定します。

3.  呼び出し[ **WdfObjectDelete** ](https://msdn.microsoft.com/library/windows/hardware/ff548734)作業項目オブジェクトを削除する場合は、ドライバーは、作業項目をもう一度キューは、作業項目を識別するハンドルが再利用できるようになりましたことを示します。 または、します。

各作業項目のコールバック関数を実行するタスクは、比較的短い形式である必要があります。 オペレーティング システムは、時間のかかるタスクを実行する作業項目のコールバック関数を使用している場合、ドライバーのシステム パフォーマンスが低下するために、システムの数に制限のワーカー スレッドを提供します。

### <a href="" id="ddk-creating-and-deleting-work-items-df"></a>作成して、作業項目の削除

ドライバーは、作成および作業項目を削除する次の 2 つの手法のいずれかを使用できます。

-   各作業項目を 1 回使用します。 必要な使用後すぐに削除すると、作業項目を作成します。

    この手法は、ドライバーを作業項目の数が少ないの頻度が低い使用 (より短い間隔分ごとに 1 回) を必要とする場合に便利です。

    たとえば、運転免許[ *EvtInterruptDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff541721)コールバック関数を呼び出すことができます[ **WdfWorkItemCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff551201)し[ **WdfWorkItemEnqueue**](https://msdn.microsoft.com/library/windows/hardware/ff551203)、および作業項目の[ *EvtWorkItem* ](https://msdn.microsoft.com/library/windows/hardware/ff541859)コールバック関数を呼び出すことができます[ **WdfObjectDelete**](https://msdn.microsoft.com/library/windows/hardware/ff548734).

    ドライバーが、このシナリオに従う場合、その[ *EvtInterruptDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff541721)コールバック関数は、ステータスを受け取る\_不十分\_からの戻り値をリソース[ **WdfWorkItemCreate**](https://msdn.microsoft.com/library/windows/hardware/ff551201)ドライバーは、システム リソース (通常はメモリ) が使用可能になるまでに必要な作業を延期できる必要があります。

-   必要に応じて、キューに再登録には、ドライバーを 1 つまたは複数の作業項目を作成します。

    この手法は、作業項目頻繁に (多くの場合、1 回以上 1 分あたり) を使用しているドライバーの便利な場合、またはドライバーの[ *EvtInterruptDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff541721)コールバック関数が状態を簡単に処理できない\_不十分\_リソースからの値を返す[ **WdfWorkItemCreate**](https://msdn.microsoft.com/library/windows/hardware/ff551201)します。

    システムは、ドライバー呼び出されるまで、ワーカー スレッドに作業項目を割り当てません[ **WdfWorkItemEnqueue**](https://msdn.microsoft.com/library/windows/hardware/ff551203)します。 そのため、システムのワーカー スレッドは、限られたリソースが場合でも、デバイスの初期化中に作業項目を作成する少量のメモリを消費がそれ以外の場合は影響しませんシステムのパフォーマンス。

    次の手順では、考えられるシナリオについて説明します。

    1.  ドライバーの[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)コールバック関数の呼び出し[ **WdfWorkItemCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff551201)作業項目のハンドルを取得します。
    2.  ドライバーの[ *EvtInterruptDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff541721)コールバック関数の作成アクションの一覧、 [ *EvtWorkItem* ](https://msdn.microsoft.com/library/windows/hardware/ff541859)コールバック関数にする必要があります実行し、呼び出します[ **WdfWorkItemEnqueue**](https://msdn.microsoft.com/library/windows/hardware/ff551203)、手順 1. からハンドルを使用します。
    3.  ドライバーの[ *EvtWorkItem* ](https://msdn.microsoft.com/library/windows/hardware/ff541859)コールバック関数は、アクションの一覧を実行し、コールバック関数が実行されていることを示すフラグを設定します。

    その後、毎回、ドライバーの[ *EvtInterruptDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff541721)コールバック関数が呼び出された場合を決定する必要があります、 [ *EvtWorkItem* ](https://msdn.microsoft.com/library/windows/hardware/ff541859)コールバック関数が実行されます。 場合、 *EvtWorkItem*コールバック関数が実行されていない、 *EvtInterruptDpc*コールバック関数を呼び出しません[ **WdfWorkItemEnqueue** ](https://msdn.microsoft.com/library/windows/hardware/ff551203)作業項目がまだキューに置かれたためです。 ここで、 *EvtInterruptDpc*コールバック関数のみのアクションのリストを更新する、 *EvtWorkItem*コールバック関数。

    各作業項目は、デバイスまたはキューに関連付けられます。 関連付けられているデバイスまたはキューが削除された場合、この手法を使用している場合、ドライバーを呼び出す必要はありませんので、すべての関連付けられている作業項目 framework 削除[ **WdfObjectDelete**](https://msdn.microsoft.com/library/windows/hardware/ff548734)します。

いくつかのドライバーを呼び出す必要があります[ **WdfWorkItemFlush** ](https://msdn.microsoft.com/library/windows/hardware/ff551204)を作業項目キューから作業項目をフラッシュします。 使用例の**WdfWorkItemFlush**メソッドのリファレンス ページを参照してください。

 

 





