---
title: I/O 要求のパラメーターの取得
description: I/O 要求のパラメーターの取得
ms.assetid: 1ba1fdcf-99bd-44e3-adbf-5dc93a790900
keywords:
- I/o 要求 WDK UMDF、パラメーターの取得
- WDK UMDF の要求処理、パラメーターの取得
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7f6f8cb1ee6c0c9ec8e9e3aed92a1de937f7061
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75208920"
---
# <a name="obtaining-parameters-for-io-requests"></a>I/O 要求のパラメーターの取得


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

ドライバーは、i/o 要求を受信すると、 [IWDFIoRequest](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiorequest)インターフェイスの次のメソッドを使用して、要求に関連するパラメーターを取得できます。

-   [**IWDFIoRequest:: GetCreateParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-getcreateparameters)または[ **IWDFIoRequest2:: getcreateparametersex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-getcreateparametersex)

-   [**IWDFIoRequest::GetDeviceIoControlParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-getdeviceiocontrolparameters)

-   [**IWDFIoRequest:: GetReadParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-getreadparameters)

-   [**IWDFIoRequest::GetWriteParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-getwriteparameters)

 

 





