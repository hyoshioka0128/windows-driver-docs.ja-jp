---
title: I/O 要求のパラメーターの取得
description: I/O 要求のパラメーターの取得
ms.assetid: 1ba1fdcf-99bd-44e3-adbf-5dc93a790900
keywords:
- I/O 要求の WDK UMDF、パラメーターを取得します。
- 要求の処理の WDK UMDF、パラメーターを取得します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10dc2f314f9e01885c27646a55804bf6bafe1d38
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375069"
---
# <a name="obtaining-parameters-for-io-requests"></a>I/O 要求のパラメーターの取得


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

I/O 要求を受信すると、ドライバー、ドライバーはの次のメソッドを使用できます、 [IWDFIoRequest](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfiorequest)要求に関連するパラメーターを取得するインターフェイス。

-   [**IWDFIoRequest::GetCreateParameters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-getcreateparameters)または[ **IWDFIoRequest2::GetCreateParametersEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest2-getcreateparametersex)

-   [**IWDFIoRequest::GetDeviceIoControlParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-getdeviceiocontrolparameters)

-   [**IWDFIoRequest::GetReadParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-getreadparameters)

-   [**IWDFIoRequest::GetWriteParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-getwriteparameters)

 

 





