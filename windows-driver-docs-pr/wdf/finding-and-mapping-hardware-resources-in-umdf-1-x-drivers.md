---
title: UMDF 1.x ドライバーでのハードウェア リソースの検索とマッピング
description: UMDF 1.x ドライバーでのハードウェア リソースの検索とマッピング
ms.assetid: 51CB254D-1B2C-43F5-925A-209810E2F5FC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ed315f412178cf4530f989fcfe63baed1a0c33a
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210744"
---
# <a name="finding-and-mapping-hardware-resources-in-umdf-1x-drivers"></a>UMDF 1.x ドライバーでのハードウェア リソースの検索とマッピング


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

UMDF バージョン2.0 以降を使用している場合は、「[ハードウェアリソースの検索とマッピング](finding-and-mapping-hardware-resources.md)」を参照してください。

UMDF 1.x ドライバーは、 [**IPnpCallbackHardware2:: On ハードウェア**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware2-onpreparehardware)コールバックメソッドでハードウェアリソースを受け取ります。 ドライバーは、 [**Iwdfcmresourcelist**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfcmresourcelist)インターフェイスを使用して、変換されたリソースリストを確認し、メモリマップトレジスタ、i/o ポート、および割り込みを識別します。

ドライバーは、 [**Iwdfcmresourcelist:: GetCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfcmresourcelist-getcount)と[**Iwdfcmresourcelist:: getdescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfcmresourcelist-getdescriptor)を呼び出すことによって、リソースリストを反復処理します。

ドライバーがメモリマップトレジスタを受け取る場合、ドライバーは[**IWDFDevice3:: MapIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice3-mapiospace)を呼び出して、レジスタにアクセスする前にレジスタをマップする必要があります。 通常、ドライバーは、そのレジスタを[**IPnpCallbackHardware2:: On hardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware2-onpreparehardware)メソッドにマップします。 ドライバーは、 [**IWDFDevice3:: UnmapIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice3-unmapiospace)を呼び出して、 [**IPnpCallbackHardware2:: onreleasehardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware2-onreleasehardware)コールバックのレジスタを解除します。 I/o ポートではマッピングは必要ないことに注意してください。

ドライバーがメモリマップトレジスタリソースを検出してマップする方法を示す例については、「 [**IWDFDevice3:: MapIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice3-mapiospace)」を参照してください。

 

 





