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
ms.openlocfilehash: 8f927a980c2079bfff843be04b7f28a1c1a7086c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558792"
---
# <a name="installing-an-audio-adapter-service-in-windows"></a>Windows で、オーディオ アダプター サービスをインストールします。

次[ **INF AddService ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546326) XYZ のオーディオ デバイスの Xyzaud.sys アダプター ドライバーがインストールされます。

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

 

 




