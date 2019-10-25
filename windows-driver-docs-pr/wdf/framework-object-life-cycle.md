---
title: フレームワーク オブジェクトのライフ サイクル
description: フレームワーク オブジェクトのライフ サイクル
ms.assetid: 33efc3a8-ac46-4626-ba0f-beb1eaa9ee47
keywords:
- フレームワークオブジェクト WDK KMDF、ライフサイクル
- ライフサイクル WDK KMDF
- フレームワークオブジェクト WDK KMDF, 作成
- 参照カウント WDK KMDF
- フレームワークオブジェクト WDK KMDF、削除
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63cd01ac5cba944730bb484e2f08e44ace760c6f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843115"
---
# <a name="framework-object-life-cycle"></a>フレームワーク オブジェクトのライフ サイクル





フレームワークオブジェクトの "ライフサイクル" は、オブジェクトが削除されたときからに対して作成されるまでの時間を範囲としています。 オブジェクトの参照カウントは、削除されるタイミングを制御します。

### <a name="creating-a-framework-object"></a>フレームワークオブジェクトの作成

ほとんどのフレームワークオブジェクトは、オブジェクトの作成メソッドへのドライバーの呼び出しによって作成されます。 たとえば、各フレームワークドライバーは、 [**Wdfdrivercreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate)を呼び出して、フレームワークドライバーオブジェクトを作成する必要があります。

その他のフレームワークオブジェクトは、フレームワークによって作成されます。 たとえば、ユーザーアプリケーションが読み取り操作または書き込み操作のためにデバイスを開くと、フレームワークによってフレームワークファイルオブジェクトが作成され、ドライバーの[*EvtDeviceFileCreate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_file_create) callback 関数に渡されます。

フレームワークまたはドライバーによって、いくつかのフレームワークオブジェクトを作成できます。 たとえば、i/o マネージャーがドライバーに i/o 要求を送信すると、フレームワークはフレームワーク要求オブジェクトを作成し、ドライバーに配信します。通常は、ドライバーの要求ハンドラーのいずれかを呼び出します。 また、ドライバーはフレームワークの要求オブジェクトを作成し、他のドライバーに配信することもできます。

### <a name="using-reference-counts"></a>参照カウントの使用

フレームワークは、各オブジェクトの参照カウントを保持します。 オブジェクトが作成されると、フレームワークはその参照カウントを1に設定します。 参照カウントがゼロになると、フレームワークによってオブジェクトが削除されます。

ドライバーでは、 [**Wdfobjectreference**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectreference)を呼び出して参照カウントまたは[**Wdfobjectreference**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectdereference)参照をインクリメントし、参照カウントをデクリメントすることで、オブジェクトの参照カウントを変更できます。 (ドライバーは、以前に**Wdfobjectdereference**を呼び出した場合にのみ、 **Wdfobjectdereference**参照を呼び出すことができます)。

ほとんどの場合、ドライバーはオブジェクトの参照カウントをインクリメントまたはデクリメントする必要がありません。 フレームワークは、オブジェクトのハンドルをドライバーに渡す前にカウントをインクリメントし、ドライバーがオブジェクトを必要としなくなったときにカウントをデクリメントします。

ドライバーが使用を終了する前に、(フレームワークまたはドライバースレッドによって) オブジェクトが削除されないようにするために、ドライバーは[**Wdfobjectreference**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectreference)を呼び出します。 ドライバーが**Wdfobjectreference**と[**Wdfobjectreference**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectdereference)参照を呼び出す必要がある状況の例については、「[送信された要求の取り消しの同期](synchronizing-cancellation-of-sent-requests.md)」を参照してください。

### <a name="deleting-a-framework-object"></a>フレームワークオブジェクトの削除

オブジェクトは削除されます。これは、ドライバーが[**Wdfobjectdelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)を呼び出すか、フレームワークが内部削除ルーチンを呼び出しますが、オブジェクトは参照カウントが0の場合にのみ削除されるためです。 ドライバーまたはフレームワークがオブジェクトを削除しようとすると、オブジェクトのハンドルは、参照カウントが0になるまで有効なままになります。 ドライバーは、 [**Wdfobjectdereference 参照**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectdereference)を呼び出してオブジェクトの参照カウントをゼロにデクリメントするだけでオブジェクトを削除する*ことはできません*。ドライバーは、 **wdfobjectdereference**も呼び出す必要があります。

フレームワークオブジェクトが親の子オブジェクトで、親が削除されている場合、フレームワークは親を削除する前に子オブジェクトを削除しようとします。 オブジェクトの削除は、親から最も遠いオブジェクトから開始され、オブジェクトの階層がルートに向かって機能します。

ドライバーは、次の2つのコールバック関数を登録できます。これらの関数は、ドライバーまたはフレームワークがオブジェクトを削除するときに、フレームワークが呼び出します。

-   [*Evtcleanupcallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup)コールバック関数。この関数は、以前に削除されるオブジェクトに対して[**Wdfobjectdereference**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectreference)を呼び出した場合に、ドライバーが[**wdfobjectdereference**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectdereference)参照を呼び出すことができるように、フレームワークによって呼び出されます。

-   フレームワークがオブジェクトの参照カウントを0にデクリメントした後に呼び出す[*Evtdestroycallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_destroy)コールバック関数。

これらのコールバック関数の1つは、オブジェクトの作成時にドライバーによって割り当てられたオブジェクト固有のリソースの割り当てを解除する必要があります。

フレームワークは、フレームワークオブジェクトの削除を常に処理し、ドライバーはこれらのオブジェクトを削除しないようにする必要があります。 ドライバーが削除できないフレームワークオブジェクトの一覧については、「 [**Wdfobjectdelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)」を参照してください。

 

 





