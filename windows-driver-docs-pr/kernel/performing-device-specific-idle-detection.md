---
title: デバイス固有のアイドル検出の実行
description: デバイス固有のアイドル検出の実行
ms.assetid: 1a4e3b66-f1dc-4dc8-af8b-ed8138270c3c
keywords:
- アイドル検出 WDK 電源管理
- デバイス固有のアイドル検出 WDK 電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c34f90a462cce823f4f7d6b1d90c05cd1a16253
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838509"
---
# <a name="performing-device-specific-idle-detection"></a>デバイス固有のアイドル検出の実行





電源マネージャーのアイドル検出ルーチンを使用する代わりに、ドライバーは、デバイス固有の条件に基づいて、独自のアイドル検出を実行できます。

このようなドライバーでは、アイドル状態のデバイスを、現在のシステム電源の状態に対して有効な最も低いスリープ状態にする必要があります。 これを行うには、ドライバーは、デバイスを移行するデバイスの電源状態を指定して、マイナー IRP コードの[**irp\_\_に\_電力を設定**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)して、電源 Irp ([**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)) を要求します。

 

 




