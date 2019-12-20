---
title: 割り込みオブジェクトの削除
description: 割り込みオブジェクトの削除
ms.assetid: B72DA452-B22F-47CD-8C5D-E741F09F556E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 659ac2e58b4cd1a9536eb179d459e46cfabf979a
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210476"
---
# <a name="deleting-an-interrupt-object"></a>割り込みオブジェクトの削除


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

ドライバーが[**IWDFDevice3:: CreateInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice3-createinterrupt)を呼び出して割り込みオブジェクトを作成した場合、ドライバーは interrupt オブジェクトを削除する必要はありません。 割り込みオブジェクトはフレームワークのデバイスオブジェクトの子オブジェクトであるため、フレームワークは割り込みオブジェクトを自動的に削除します。

フレームワークでは、次の規則が使用されます。

-   ドライバーが[**Onのハードウェア**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware2-onpreparehardware)コールバックメソッドから[**createinterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice3-createinterrupt)を呼び出すと、ドライバーが[**onpreparehardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware2-onreleasehardware)コールバックから復帰した後に、その割り込みオブジェクトが削除されます。

-   ドライバーが[**Ondeviceadd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)コールバックメソッドから[**createinterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice3-createinterrupt)を呼び出した場合、デバイスが削除されると、フレームワークは割り込みオブジェクトを削除します。

必要に応じて、ドライバーは[**Iwdfobject::D eletewdfobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfobject-deletewdfobject)を呼び出して、割り込みオブジェクトをいつでも削除できます。 ドライバーは、 [**Ondeviceadd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)または[**onてハードウェア**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware2-onpreparehardware)の外部で新しい割り込みオブジェクトを作成することはできないため、オブジェクトを削除する前に、ドライバーがオブジェクトを削除する必要がない限り、手動でオブジェクトを削除する必要はありません。

 

 





