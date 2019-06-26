---
title: デバイス固有のアイドル状態検出の実行
description: デバイス固有のアイドル状態検出の実行
ms.assetid: 1a4e3b66-f1dc-4dc8-af8b-ed8138270c3c
keywords:
- アイドル状態検出 WDK 電源管理
- デバイスに固有のアイドル状態検出 WDK 電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6f1784492aba54d97286929ee7c39a4236afccb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384741"
---
# <a name="performing-device-specific-idle-detection"></a>デバイス固有のアイドル状態検出の実行





電源マネージャーのアイドル状態の検出ルーチンを使用する代わりに、ドライバーは、デバイスに固有の条件に基づいて、独自のアイドル状態検出を実行できます。

このようなドライバーは、現在のシステム電源の状態に対して有効な最小の可能なスリープ状態で、アイドル状態のデバイスを配置する必要があります。 ドライバーが IRP の電源を要求を行うに ([**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-porequestpowerirp)) IRP コードの軽微なと[ **IRP\_MN\_設定\_POWER**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)デバイスの電源状態をデバイスに移行する必要がありますを指定します。

 

 




