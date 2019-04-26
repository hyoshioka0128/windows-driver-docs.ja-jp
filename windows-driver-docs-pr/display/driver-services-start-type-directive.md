---
title: ドライバー\サービスの開始の種類ディレクティブ
description: "\"Driver\\services\"開始の type ディレクティブは、すべてのディスプレイ ドライバーのサービスのインストールの設定要件です。 Windows Display Driver Model (WDDM) ドライバーがプラグ アンド プレイ (PnP) およびしたがって必要がありますオンデマンド起動、場所 StartType = 3。"
ms.assetid: 1B34DC18-EA81-44DB-B60A-D05B685E9321
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45e44b96055fcb0dad24a65f9db00f56182138be
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358440"
---
# <a name="driverservices-start-type-directive"></a>ドライバー\\サービスは、type ディレクティブを開始します。


*ドライバー\\サービス*開始 type ディレクティブがすべてのディスプレイ ドライバーのサービスのインストールの設定要件。 Windows Display Driver Model (WDDM) ドライバーがプラグ アンド プレイ (PnP) およびしたがって必要がありますオンデマンド起動、場所*StartType* = 3。

次に、例を示します。

``` syntax
; Service Installation Section
;

[R200_Service_Inst]
ServiceType    = 1                  ; SERVICE_KERNEL_DRIVER
StartType      = 3                  ; SERVICE_DEMAND_START
ErrorControl   = 0                  ; SERVICE_ERROR_IGNORE
LoadOrderGroup = Video
ServiceBinary  = %12%\r200.sys
```

 

 





