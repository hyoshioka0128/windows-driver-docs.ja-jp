---
title: 割り込みオブジェクトの削除
description: 割り込みオブジェクトの削除
ms.assetid: B72DA452-B22F-47CD-8C5D-E741F09F556E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3bedae105a3faf78c386cb20bd21bdb81fd1f4bd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377466"
---
# <a name="deleting-an-interrupt-object"></a>割り込みオブジェクトの削除


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

ドライバーは、呼び出すことによって、割り込みオブジェクトを作成する場合[ **IWDFDevice3::CreateInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice3-createinterrupt)ドライバーは、割り込みオブジェクトを削除する必要はありません。 フレームワークは、割り込みオブジェクトは、framework デバイス オブジェクトの子オブジェクトでは自動的に割り込みオブジェクトを削除します。

フレームワークは、次の規則を使用します。

-   ドライバーを呼び出す場合[ **CreateInterrupt** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice3-createinterrupt)からその[ **OnPrepareHardware** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallbackhardware2-onpreparehardware)コールバック メソッド、フレームワークは、割り込みを削除します。オブジェクトから、ドライバーが返された後にその[ **OnReleaseHardware** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallbackhardware2-onreleasehardware)コールバック。

-   ドライバーを呼び出す場合[ **CreateInterrupt** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice3-createinterrupt)からその[ **OnDeviceAdd** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)コールバック メソッド、フレームワークは、割り込みオブジェクトを削除します。デバイスが削除されたとき。

ドライバーを呼び出すことができます必要に応じて、 [ **IWDFObject::DeleteWdfObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfobject-deletewdfobject)割り込みオブジェクトをいつでも削除します。 ドライバーは、外側の新しい割り込みオブジェクトを作成できないため[ **OnDeviceAdd** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)または[ **OnPrepareHardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallbackhardware2-onpreparehardware)、手動で削除した、フレームワークは、それを削除する前に、ドライバーは、オブジェクトを削除する必要がありますしない限り、オブジェクトを使用しない必要があります。

 

 





