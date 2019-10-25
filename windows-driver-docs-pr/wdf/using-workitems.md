---
title: 作業項目の使用
description: 作業項目の使用
ms.assetid: 4617A33F-9026-45FF-9CC2-7215423E6D35
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f430d389ec7586312a94b1399273be6b212283a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842590"
---
# <a name="using-work-items"></a>作業項目の使用


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

作業項目は、ドライバーが[*Onworkitem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfworkitem/nc-wudfworkitem-wudf_workitem_function)イベントコールバック関数で実行するタスクです。 これらの関数は、非同期的に実行します。

複数のデバイスで割り込み線が共有される可能性があるため、 [*OnInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_isr)で割り込みサービス要求 (ISR) の実行を遅らせずに追加の処理を実行する必要がある場合、UMDF ドライバーは通常、作業項目を使用します。

通常、ドライバーの[*OnInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_isr)コールバック関数は、作業項目オブジェクトを作成し、それをシステムの作業項目キューに追加します。 その後、threadpool スレッドによってオブジェクトがデキューされ、作業項目の[*Onworkitem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfworkitem/nc-wudfworkitem-wudf_workitem_function)コールバック関数が呼び出されます。

## <a name="setting-up-a-work-item"></a>作業項目の設定


作業項目を設定するには、次の操作を行う必要があります。

1.  作業項目を作成します。

    ドライバーは[**IWDFDevice3:: CreateWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice3-createworkitem)を呼び出して、作業項目オブジェクトを作成し、作業項目を処理する[*onworkitem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfworkitem/nc-wudfworkitem-wudf_workitem_function)コールバック関数を識別します。

2.  作業項目に関する情報を格納します。

    通常、ドライバーは、作業項目オブジェクトのコンテキストメモリを使用して、 [*Onworkitem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfworkitem/nc-wudfworkitem-wudf_workitem_function)コールバック関数が実行するタスクに関する情報を格納します。 *Onworkitem*コールバック関数が呼び出されると、このコンテキストメモリにアクセスすることによって情報を取得できます。 コンテキストメモリを割り当ててアクセスする方法の詳細については、「[**Iwdfobject:: 割り当てコンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfobject-assigncontext)」を参照してください。

3.  作業項目をシステムの作業項目キューに追加します。

    ドライバーは[**Iwdfworkitem:: エンキュー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfworkitem-enqueue)を呼び出します。これにより、ドライバーの作業項目が作業項目キューに追加されます。

ドライバーが[**IWDFDevice3:: CreateWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice3-createworkitem)を呼び出すと、必要に応じて親オブジェクト (デバイスオブジェクト、キューオブジェクトなど) を指定できます。 そのオブジェクトを削除すると、そのオブジェクトに関連付けられている既存の作業項目もすべて削除されます。

## <a name="using-the-workitem-callback-function"></a>WorkItem コールバック関数の使用


作業項目キューに追加された作業項目は、システムワーカースレッドが使用可能になるまでキューに残ります。 システムワーカースレッドは、キューから作業項目を削除した後、ドライバーの OnWorkItem コールバック関数を呼び出して、作業項目オブジェクトを入力として渡します。

通常、OnWorkItem コールバック関数は、次の手順を実行します。

1.  作業項目オブジェクトのコンテキストメモリにアクセスすることによって、作業項目に関するドライバーから提供される情報を取得します。
2.  指定したタスクを実行します。 必要に応じて、コールバック関数は[**Iwdfworkitem:: GetParentObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfworkitem-getparentobject)を呼び出して、作業項目の親オブジェクトを決定できます。
3.  ドライバーが作業項目をキューへする場合は、作業項目へのハンドルを再利用できるようになったことを示します。

一部のドライバーでは、作業項目キューから作業項目をフラッシュするために[**Iwdfworkitem:: Flush**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfworkitem-flush)を呼び出す必要がある場合があります。 ドライバーが**Flush**メソッドを呼び出すと、メソッドは、ワーカースレッドが作業項目キューから指定された作業項目を削除し、ドライバーの[*onworkitem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfworkitem/nc-wudfworkitem-wudf_workitem_function)コールバック関数と*onworkitem*コールバックを呼び出した後に、を返しません。その後、作業項目の処理後に関数が返されます。

 

 





