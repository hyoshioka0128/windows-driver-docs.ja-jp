---
title: UPS ミニドライバーの機能
description: UPS ミニドライバーの機能
ms.assetid: a93dbada-bcf7-4963-ba57-c6db5922c66b
keywords:
- UPS ミニドライバー WDK, 機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d558da26414534e54ee86fb10c56df6fa59439ba
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833961"
---
# <a name="ups-minidriver-functionality"></a>UPS ミニドライバーの機能


## <span id="ddk_ups_minidriver_functionality_kg"></span><span id="DDK_UPS_MINIDRIVER_FUNCTIONALITY_KG"></span>


UPS ミニドライバーは、システム提供の UPS サービスによって呼び出される次の一連の関数をエクスポートする必要があります。

-   [**UPSInit**](https://docs.microsoft.com/windows-hardware/drivers/ddi/upssvc/nf-upssvc-upsinit)

-   [**UPSGetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/upssvc/nf-upssvc-upsgetstate)

-   [**UPSWaitForStateChange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/upssvc/nf-upssvc-upswaitforstatechange)

-   [**UPSCancelWait**](https://docs.microsoft.com/windows-hardware/drivers/ddi/upssvc/nf-upssvc-upscancelwait)

-   [**Up・ Noff**](https://docs.microsoft.com/windows-hardware/drivers/ddi/upssvc/nf-upssvc-upsturnoff)

-   [**UPSStop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/upssvc/nf-upssvc-upsstop)

さらに、Microsoft Windows SDK のドキュメントで説明されているように、ミニドライバーは[**DLLMain**](https://docs.microsoft.com/windows/desktop/Dlls/dllmain)関数をエクスポートする必要があります。

これらの関数をエクスポートするだけでなく、ミニドライバーは[ups レジストリエントリ](ups-registry-entries.md)の初期値を指定し、必要に応じて値を変更して、ups の状態の変更を反映する必要があります。

通常、UPS ミニドライバーは、 [**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)、 [**ReadFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-readfile)、および[**WriteFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-writefile)関数 (Windows SDK ドキュメントで説明) を呼び出すことによって、COM ポートを介して ups ユニットと通信します。 ミニドライバーは、UPS ユニットがサポートするすべての通信プロトコルを実装する役割を担います。

 

 




