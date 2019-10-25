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
ms.openlocfilehash: f09b05eb5a77fbe3029ed982721d4827055da297
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844481"
---
# <a name="storage-filter-drivers-adddevice-routine"></a>記憶域フィルター ドライバーの AddDevice ルーチン


## <span id="ddk_storage_filter_driver_s_adddevice_routine_kg"></span><span id="DDK_STORAGE_FILTER_DRIVER_S_ADDDEVICE_ROUTINE_KG"></span>


PnP マネージャーは、そのドライバーによって制御されるデバイスを検出したときに、記憶域フィルタードライバーの[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンを呼び出します。 記憶域フィルタードライバー (SFD) の*AddDevice*ルーチンは、ストレージクラスドライバーのルーチンに似ていますが、デバイス (SRB\_関数\_の要求\_デバイス) を要求しない点が異なります。

ストレージクラスドライバーの[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンの詳細については、「[ストレージクラスドライバー](storage-class-drivers.md)」を参照してください。 PnP ドライバーの*AddDevice*ルーチンに関する一般的な情報については、「[プラグアンドプレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)」を参照してください。

 

 




