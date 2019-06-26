---
title: オーディオ アダプター サービスをインストールします。
description: オーディオ アダプター サービスをインストールします。
ms.assetid: 465005da-bf06-497b-801c-fe5aa19a3974
keywords:
- オーディオ アダプター WDK、サービスのインストール
- アダプターのドライバー WDK オーディオ、サービスのインストール
- ポート クラス オーディオ アダプター WDK、サービスのインストール
- アダプター サービスの WDK オーディオ
ms.date: 10/26/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69fab800bc97d16bc70d0579eb365d802547e367
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359893"
---
# <a name="installing-an-audio-adapter-service-in-windows"></a>Windows でのオーディオ アダプター サービスのインストール

次[ **INF AddService ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addservice-directive) XYZ のオーディオ デバイスの Xyzaud.sys アダプター ドライバーがインストールされます。

```cpp
  [XYZ-Audio-Device.Services.NTX86]
  AddService = XYZ-Audio-Device, 0x00000002, XYZ-Audio-Device.Service.Install

  [XYZ-Audio-Device.Service.Install]
  DisplayName   = %XYZ-Audio-Device.ServiceDescription%
  ServiceType   = 1                  ; SERVICE_KERNEL_DRIVER
  StartType     = 3                  ; SERVICE_DEMAND_START
  ErrorControl  = 1                  ; SERVICE_ERROR_NORMAL
  ServiceBinary = %12%\system32\drivers\xyzaud.sys
```

 

 




