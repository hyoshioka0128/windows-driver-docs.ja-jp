---
title: 割り込みオブジェクトの削除
description: 割り込みオブジェクトの削除
ms.assetid: B72DA452-B22F-47CD-8C5D-E741F09F556E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9625d41546177ad6d6dc8ed49d0a97ea75284d32
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841758"
---
# <a name="deleting-an-interrupt-object"></a>割り込みオブジェクトの削除


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

ドライバーが[**IWDFDevice3:: CreateInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice3-createinterrupt)を呼び出して割り込みオブジェクトを作成した場合、ドライバーは interrupt オブジェクトを削除する必要はありません。 割り込みオブジェクトはフレームワークのデバイスオブジェクトの子オブジェクトであるため、フレームワークは割り込みオブジェクトを自動的に削除します。

フレームワークでは、次の規則が使用されます。

-   ドライバーが[**Onのハードウェア**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware2-onpreparehardware)コールバックメソッドから[**createinterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice3-createinterrupt)を呼び出すと、ドライバーが[**onpreparehardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware2-onreleasehardware)コールバックから復帰した後に、その割り込みオブジェクトが削除されます。

-   ドライバーが[**Ondeviceadd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)コールバックメソッドから[**createinterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice3-createinterrupt)を呼び出した場合、デバイスが削除されると、フレームワークは割り込みオブジェクトを削除します。

必要に応じて、ドライバーは[**Iwdfobject::D eletewdfobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfobject-deletewdfobject)を呼び出して、割り込みオブジェクトをいつでも削除できます。 ドライバーは、 [**Ondeviceadd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)または[**onてハードウェア**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware2-onpreparehardware)の外部で新しい割り込みオブジェクトを作成することはできないため、オブジェクトを削除する前に、ドライバーがオブジェクトを削除する必要がない限り、手動でオブジェクトを削除する必要はありません。

 

 





