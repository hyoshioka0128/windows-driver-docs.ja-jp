---
title: I/O 要求のパラメーターの取得
description: I/O 要求のパラメーターの取得
ms.assetid: 1ba1fdcf-99bd-44e3-adbf-5dc93a790900
keywords:
- I/O 要求の WDK UMDF、パラメーターを取得します。
- 要求の処理の WDK UMDF、パラメーターを取得します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc2b548e9d319346afa33c8743476f8c8462552d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581631"
---
# <a name="obtaining-parameters-for-io-requests"></a>I/O 要求のパラメーターの取得


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

I/O 要求を受信すると、ドライバー、ドライバーはの次のメソッドを使用できます、 [IWDFIoRequest](https://msdn.microsoft.com/library/windows/hardware/ff558985)要求に関連するパラメーターを取得するインターフェイス。

-   [**IWDFIoRequest::GetCreateParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff559088)または[ **IWDFIoRequest2::GetCreateParametersEx**](https://msdn.microsoft.com/library/windows/hardware/ff558989)

-   [**IWDFIoRequest::GetDeviceIoControlParameters**](https://msdn.microsoft.com/library/windows/hardware/ff559095)

-   [**IWDFIoRequest::GetReadParameters**](https://msdn.microsoft.com/library/windows/hardware/ff559113)

-   [**IWDFIoRequest::GetWriteParameters**](https://msdn.microsoft.com/library/windows/hardware/ff559130)

 

 





