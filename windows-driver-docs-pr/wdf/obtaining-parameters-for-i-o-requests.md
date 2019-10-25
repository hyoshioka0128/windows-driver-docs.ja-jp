---
title: I/O 要求のパラメーターの取得
description: I/O 要求のパラメーターの取得
ms.assetid: 1ba1fdcf-99bd-44e3-adbf-5dc93a790900
keywords:
- I/o 要求 WDK UMDF、パラメーターの取得
- WDK UMDF の要求処理、パラメーターの取得
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47247a5c5d8aa9064763b2abea8e5741de420ab3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843136"
---
# <a name="obtaining-parameters-for-io-requests"></a>I/O 要求のパラメーターの取得


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

ドライバーは、i/o 要求を受信すると、 [IWDFIoRequest](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiorequest)インターフェイスの次のメソッドを使用して、要求に関連するパラメーターを取得できます。

-   [**IWDFIoRequest:: GetCreateParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-getcreateparameters)または[ **IWDFIoRequest2:: getcreateparametersex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-getcreateparametersex)

-   [**IWDFIoRequest::GetDeviceIoControlParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-getdeviceiocontrolparameters)

-   [**IWDFIoRequest:: GetReadParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-getreadparameters)

-   [**IWDFIoRequest::GetWriteParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-getwriteparameters)

 

 





