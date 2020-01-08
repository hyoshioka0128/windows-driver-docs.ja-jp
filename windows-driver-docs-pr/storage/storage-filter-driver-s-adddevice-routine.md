---
title: 記憶域フィルター ドライバーの AddDevice ルーチン
description: 記憶域フィルター ドライバーの AddDevice ルーチン
ms.assetid: 7970fb3e-4e4c-4ff7-9738-e09454a864c4
keywords:
- ストレージフィルタードライバー WDK、AddDevice
- フィルタードライバー WDK storage、AddDevice
- SFD WDK storage、AddDevice
- AddDevice ルーチン WDK storage
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 158c53a70c2e24eaec63d795d5a91776c5b21ee7
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606470"
---
# <a name="storage-filter-drivers-adddevice-routine"></a>記憶域フィルター ドライバーの AddDevice ルーチン

PnP マネージャーは、そのドライバーによって制御されるデバイスを検出したときに、記憶域フィルタードライバーの[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンを呼び出します。 記憶域フィルタードライバー (SFD) の AddDevice ルーチンは、デバイス (SRB_FUNCTION_CLAIM_DEVICE) を要求しないことを除けば、記憶域クラスドライバーのルーチンと似ています。

ストレージクラスドライバーの[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンの詳細については、「[ストレージクラスドライバー](introduction-to-storage-class-drivers.md)」を参照してください。 PnP ドライバーの*AddDevice*ルーチンに関する一般的な情報については、「[プラグアンドプレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)」を参照してください。
