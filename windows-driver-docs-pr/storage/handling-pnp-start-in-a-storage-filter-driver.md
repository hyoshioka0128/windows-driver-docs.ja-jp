---
title: 記憶域フィルター ドライバーでの PnP 開始の処理
description: 記憶域フィルター ドライバーでの PnP 開始の処理
ms.assetid: 02a87fec-772d-4416-bd3a-5c7f98e8d55e
keywords:
- ストレージフィルタードライバー WDK、PnP
- フィルタードライバー WDK storage、PnP
- SFD WDK storage、PnP
- PnP WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f21e1473326d24647bfce864683b94600648eba
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606518"
---
# <a name="handling-pnp-start-in-a-storage-filter-driver"></a>記憶域フィルター ドライバーでの PnP 開始の処理

ストレージフィルタードライバー (SFD) は、デバイス固有の初期化を実行し、PnP マネージャーが開始要求を使用して[*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンを呼び出したときに、デバイス拡張機能を設定します ([**irp\_MJ\_pnp**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)を使用した pnp [ **\_\_デバイスの起動\_開始**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)します)。 SFD は、ストレージクラスドライバーとほぼ同じように開始要求を処理します。

ストレージクラスドライバーが開始要求を処理し、そのデバイス拡張機能を設定する方法の詳細については、「[ストレージクラスドライバー](introduction-to-storage-class-drivers.md)」を参照してください。 PnP 開始要求の処理に関する一般的な情報については、「[プラグアンドプレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)」を参照してください。
