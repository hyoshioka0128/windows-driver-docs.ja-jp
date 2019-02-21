---
title: Driver\services は、type ディレクティブを開始します。
description: "\"Driver\\services\"開始の type ディレクティブは、すべてのディスプレイ ドライバーのサービスのインストールの設定要件です。 Windows Display Driver Model (WDDM) ドライバーがプラグ アンド プレイ (PnP) およびしたがって必要がありますオンデマンド起動、場所 StartType = 3。"
ms.assetid: 1B34DC18-EA81-44DB-B60A-D05B685E9321
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45e44b96055fcb0dad24a65f9db00f56182138be
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551342"
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

 

 





