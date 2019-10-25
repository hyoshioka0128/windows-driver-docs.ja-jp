---
title: 記憶域フィルター ドライバーの DriverEntry ルーチン
description: 記憶域フィルター ドライバーの DriverEntry ルーチン
ms.assetid: 801daf42-259d-45ab-a5c5-88acb2d35bef
keywords:
- ストレージフィルタードライバー WDK、DriverEntry
- フィルタードライバー WDK storage、DriverEntry
- SFD WDK storage、DriverEntry
- DriverEntry WDK storage
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55662a9d5c8db817bd9ee0c205df2f002cb9a5ad
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844473"
---
# <a name="storage-filter-drivers-driverentry-routine"></a>記憶域フィルター ドライバーの DriverEntry ルーチン


## <span id="ddk_storage_filter_drivers_driverentry_routine_kg"></span><span id="DDK_STORAGE_FILTER_DRIVERS_DRIVERENTRY_ROUTINE_KG"></span>


他のカーネルモードドライバーと同様に、ストレージフィルタードライバー (SFD) の[*Driverentry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンでは、入力ドライバーオブジェクトのディスパッチとその他のエントリポイントを定義する必要があります。 必要に応じて、SFD は[**Ioallocatedriverobjectextension**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocatedriverobjectextension)を呼び出して適切なサイズのドライバーオブジェクト拡張を割り当て、後で使用できるように入力レジストリパスをドライバ拡張にコピーして、ドライバー拡張機能を他のもので初期化することができます。ドライバーによって決定されたデータ (存在する場合)。

PnP ドライバーの[*Driverentry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンの詳細については、「[プラグアンドプレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)」を参照してください。

 

 




