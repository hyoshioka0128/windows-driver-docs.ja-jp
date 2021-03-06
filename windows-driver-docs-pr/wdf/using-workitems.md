---
title: 作業項目の使用
description: 作業項目の使用
ms.assetid: 4617A33F-9026-45FF-9CC2-7215423E6D35
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d2a7ea275fc418d2b83b20b280cee38184de7d1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372164"
---
# <a name="using-work-items"></a>作業項目の使用


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

作業項目は、ドライバーで実行するタスク、 [ *OnWorkItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfworkitem/nc-wudfworkitem-wudf_workitem_function)イベント コールバック関数。 これらの関数を非同期的に実行します。

場合に UMDF ドライバーが作業項目によく使用して、 [ *OnInterruptIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_isr)割り込み行があるので、割り込みサービス要求 (ISR) の実行を遅らせることがなく追加の処理を実行する必要があります複数のデバイスで共有されます。

通常、ドライバーの[ *OnInterruptIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_isr)コールバック関数は、作業項目オブジェクトを作成し、システムの作業項目のキューに追加します。 その後、スレッド プールのスレッドのデキュー オブジェクトと呼び出し、作業項目の[ *OnWorkItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfworkitem/nc-wudfworkitem-wudf_workitem_function)コールバック関数。

## <a name="setting-up-a-work-item"></a>作業項目の設定


作業項目を設定するには、ドライバーが必要です。

1.  作業項目を作成します。

    ドライバーの呼び出し[ **IWDFDevice3::CreateWorkItem** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice3-createworkitem)作業項目オブジェクトを作成して、識別するために、 [ *OnWorkItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfworkitem/nc-wudfworkitem-wudf_workitem_function)コールバック作業項目を処理する関数。

2.  作業項目に関する情報を格納します。

    通常、ドライバーを使用して作業項目オブジェクトのコンテキストのメモリ タスクに関する情報を格納する、 [ *OnWorkItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfworkitem/nc-wudfworkitem-wudf_workitem_function)コールバック関数を実行する必要があります。 ときに、 *OnWorkItem*コールバック関数が呼び出されると、このコンテキストのメモリにアクセスして、情報を取得できます。 割り当てるし、コンテキストのメモリにアクセスする方法については、次を参照してください。[**IWDFObject::AssignContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfobject-assigncontext)します。

3.  システムの作業項目のキューに作業項目を追加します。

    ドライバーの呼び出し[ **IWDFWorkItem::Enqueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfworkitem-enqueue)、作業項目のキューに、ドライバーの作業項目を追加します。

ドライバーを呼び出すと[ **IWDFDevice3::CreateWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice3-createworkitem)、親オブジェクト (たとえば、デバイス オブジェクトまたはキュー オブジェクト) を必要に応じて指定することがあります。 システムでは、そのオブジェクトを削除したときにも、オブジェクトに関連付けられている既存の作業項目を削除します。

## <a name="using-the-workitem-callback-function"></a>作業項目のコールバック関数の使用


作業項目は、作業項目のキューに追加されたが、システムのワーカー スレッドが使用可能になるまで、キューに保持されます。 システム ワーカー スレッドでは、キューから作業項目を削除、入力として、作業項目オブジェクトを渡して、ドライバーの OnWorkItem コールバック関数を呼び出します。

通常、OnWorkItem のコールバック関数は、次の手順を実行します。

1.  作業項目オブジェクトのコンテキストのメモリにアクセスすることには、作業項目に関するドライバーによって提供される情報を取得します。
2.  指定したタスクを実行します。 かどうか、必要に応じて、コールバック関数は、呼び出して[ **IWDFWorkItem::GetParentObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfworkitem-getparentobject)作業項目の親オブジェクトを決定します。
3.  場合は、ドライバーは、作業項目をもう一度キューは、作業項目を識別するハンドルが再利用できるようになりましたことを示します。

いくつかのドライバーを呼び出す必要があります[ **IWDFWorkItem::Flush** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfworkitem-flush)を作業項目キューから作業項目をフラッシュします。 ドライバーを呼び出す場合、**フラッシュ**メソッド、メソッドまで制御を戻しませんワーカー スレッドが作業項目のキューから指定された作業項目を削除し、ドライバーのと呼ばれる[ *OnWorkItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfworkitem/nc-wudfworkitem-wudf_workitem_function)コールバック関数、および*OnWorkItem*コールバック関数が、作業項目の処理後に返された後です。

 

 





