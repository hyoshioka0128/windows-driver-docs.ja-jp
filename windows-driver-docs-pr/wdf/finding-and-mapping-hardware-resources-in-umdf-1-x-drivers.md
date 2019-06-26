---
title: UMDF 1.x ドライバーでのハードウェア リソースの検索とマッピング
description: UMDF 1.x ドライバーでのハードウェア リソースの検索とマッピング
ms.assetid: 51CB254D-1B2C-43F5-925A-209810E2F5FC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eea8153e4841644dad27bb2cb165312318670a7e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368714"
---
# <a name="finding-and-mapping-hardware-resources-in-umdf-1x-drivers"></a>UMDF 1.x ドライバーでのハードウェア リソースの検索とマッピング


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

UMDF バージョン 2.0 以降を使用している場合は、次を参照してください。[マッピング ハードウェア リソースの検索と](finding-and-mapping-hardware-resources.md)します。

1\.x UMDF ドライバー内のハードウェア リソースを受け取るその[ **IPnpCallbackHardware2::OnPrepareHardware** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallbackhardware2-onpreparehardware)コールバック メソッド。 ドライバーを使用して、 [ **IWDFCmResourceList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfcmresourcelist)インターフェイスを翻訳済みのリソースの一覧を確認し、メモリ マップト レジスタ、I/O ポート、および割り込みを特定します。

ドライバーは、呼び出すことによって、リソースのリストを反復処理[ **IWDFCmResourceList::GetCount** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfcmresourcelist-getcount)と[ **IWDFCmResourceList::GetDescriptor** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfcmresourcelist-getdescriptor).

ドライバーは、メモリ マップト レジスタを受信する場合、ドライバーを呼び出す必要があります[ **IWDFDevice3::MapIoSpace** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice3-mapiospace)それらにアクセスできる前に、レジスタにマップします。 通常、ドライバーはマップでのレジスタの[ **IPnpCallbackHardware2::OnPrepareHardware** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallbackhardware2-onpreparehardware)メソッド。 ドライバーでのレジスタの割り当てを解除、 [ **IPnpCallbackHardware2::OnReleaseHardware** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallbackhardware2-onreleasehardware)呼び出すことによってコールバック[ **IWDFDevice3::UnmapIoSpace** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice3-unmapiospace). I/O ポートのマッピングは必要ないことに注意してください。

例については、ドライバーを検索し、メモリ マップト マップ リソースを登録する方法を示しますが、次を参照してください。 [ **IWDFDevice3::MapIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice3-mapiospace)します。

 

 





