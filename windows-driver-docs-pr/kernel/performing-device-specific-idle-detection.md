---
title: デバイスに固有のアイドル状態の検出を実行します。
description: デバイスに固有のアイドル状態の検出を実行します。
ms.assetid: 1a4e3b66-f1dc-4dc8-af8b-ed8138270c3c
keywords:
- アイドル状態検出 WDK 電源管理
- デバイスに固有のアイドル状態検出 WDK 電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39749616b5348b6415eb2c6c7a52d13b693c0c64
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539269"
---
# <a name="performing-device-specific-idle-detection"></a>デバイスに固有のアイドル状態の検出を実行します。





電源マネージャーのアイドル状態の検出ルーチンを使用する代わりに、ドライバーは、デバイスに固有の条件に基づいて、独自のアイドル状態検出を実行できます。

このようなドライバーは、現在のシステム電源の状態に対して有効な最小の可能なスリープ状態で、アイドル状態のデバイスを配置する必要があります。 ドライバーが IRP の電源を要求を行うに ([**PoRequestPowerIrp**](https://msdn.microsoft.com/library/windows/hardware/ff559734)) IRP コードの軽微なと[ **IRP\_MN\_設定\_POWER**](https://msdn.microsoft.com/library/windows/hardware/ff551744)デバイスの電源状態をデバイスに移行する必要がありますを指定します。

 

 




