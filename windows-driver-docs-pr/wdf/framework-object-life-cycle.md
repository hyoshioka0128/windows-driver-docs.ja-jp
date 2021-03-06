---
title: フレームワーク オブジェクトのライフ サイクル
description: フレームワーク オブジェクトのライフ サイクル
ms.assetid: 33efc3a8-ac46-4626-ba0f-beb1eaa9ee47
keywords:
- framework オブジェクト WDK KMDF、ライフ サイクル
- WDK KMDF のライフ サイクル
- framework のオブジェクトを作成する、WDK KMDF
- 参照カウントの WDK KMDF
- framework のオブジェクトを削除する、WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 358095c96a619fcdabd591024615a321b0086b40
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384456"
---
# <a name="framework-object-life-cycle"></a>フレームワーク オブジェクトのライフ サイクル





Framework オブジェクトの「ライフ サイクル」は、削除されるときに、オブジェクトの作成時から時間をまたがっています。 オブジェクトの参照カウント コントロールが削除されるときにします。

### <a name="creating-a-framework-object"></a>Framework オブジェクトを作成します。

ほとんどのフレームワーク オブジェクトは、オブジェクトの作成方法のドライバーの呼び出しによって作成されます。 たとえば、各フレームワーク ドライバーを呼び出す必要があります[ **WdfDriverCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nf-wdfdriver-wdfdrivercreate)フレームワーク ドライバー オブジェクトを作成します。

その他のフレームワーク オブジェクトは、フレームワークによって作成されます。 たとえば、ユーザーのアプリケーションでのデバイスを開くと読み取りまたは書き込み操作、フレームワークが framework ファイル オブジェクトを作成し、ドライバーに渡します[ *EvtDeviceFileCreate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_file_create)コールバック関数。

いずれか、フレームワークによって、またはドライバーによって、いくつかのフレームワーク オブジェクトを作成できます。 たとえば、I/O マネージャーは、ドライバー、I/O 要求を配信するときにフレームワークはフレームワーク要求オブジェクトを作成しに配信、ドライバーでは、通常、ドライバーの要求ハンドラーの 1 つを呼び出すことによって。 ドライバーは framework 要求オブジェクトを作成し、その他のドライバーに配信できます。

### <a name="using-reference-counts"></a>参照を使用してカウントします。

フレームワークは、各オブジェクトの参照カウントを保持します。 オブジェクトが作成されたときに、フレームワークは、1 つに、参照カウントを設定します。 参照カウントには、0 になると、フレームワークは、オブジェクトを削除します。

ドライバーは、呼び出すことによって、オブジェクトの参照カウントを変更できます[ **WdfObjectReference** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectreference)参照カウントをインクリメントするまたは[ **WdfObjectDereference**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectdereference)参照カウントをデクリメントします。 (ドライバーが呼び出せる**WdfObjectDereference**が以前に呼び出された場合にのみ**WdfObjectReference**)。

ほとんどの場合、ドライバーはインクリメントまたはオブジェクトの参照カウントをデクリメントする必要はありません。 フレームワーク カウントをインクリメント数を渡す前に、オブジェクトのハンドルと、ドライバーでは、デクリメント、ドライバーが不要になったオブジェクトを必要がある場合。

ドライバー呼び出し[ **WdfObjectReference** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectreference)オブジェクトは削除しないようにする (フレームワークまたはドライバーのスレッドによって) を使用して、ドライバーを完了する前にします。 ドライバーが呼び出す必要があります例ような状況の**WdfObjectReference**と[ **WdfObjectDereference**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectdereference)を参照してください[送信の取り消しを同期します。要求](synchronizing-cancellation-of-sent-requests.md)します。

### <a name="deleting-a-framework-object"></a>Framework のオブジェクトを削除します。

オブジェクトは、ドライバーを呼び出すため、削除された[ **WdfObjectDelete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete)またはフレームワークは、内部削除ルーチンを呼び出しますが、参照カウントが 0 の場合にのみ、オブジェクトが削除されたためです。 ドライバーやフレームワークは、オブジェクトを削除しようとしましたが、後に、オブジェクトのハンドルの値は、参照カウントがゼロになった後まで有効です。 ドライバー*できません*オブジェクトを呼び出すだけで削除[ **WdfObjectDereference** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectdereference) 0 - オブジェクトの参照カウントをデクリメントするドライバー呼び出す必要がありますも**WdfObjectDelete**します。

Framework オブジェクトの親の子オブジェクトである親が削除されている場合は、フレームワークは、親を削除する前に、子オブジェクトを削除しようとします。 オブジェクトの削除は、惑星の親オブジェクトから開始し、オブジェクト階層のルートに向かってを動作します。

ドライバーは、ドライバーやフレームワークがオブジェクトを削除するときにフレームワークから呼び出される次の 2 つのコールバック関数を登録できます。

-   [ *EvtCleanupCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup)コールバック関数は、フレームワーク、ドライバーを呼び出せるように[ **WdfObjectDereference** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectdereference)場合以前と呼ばれていた[ **WdfObjectReference** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectreference)オブジェクトの削除中です。

-   [ *EvtDestroyCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nc-wdfobject-evt_wdf_object_context_destroy)コールバック関数では、フレームワークを呼び出した後、オブジェクトの参照カウントがゼロにデクリメントされています。

これらのコールバック関数のいずれかのオブジェクトが作成されたときに、ドライバーが割り当てられているオブジェクトに固有のリソースの割り当てを解除する必要があります。

フレームワークは、常に、フレームワークの一部のオブジェクトの削除を処理して、ドライバーがこれらのオブジェクトを削除しないでください。 ドライバーを削除できません framework オブジェクトの一覧は、次を参照してください。 [ **WdfObjectDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete)します。

 

 





