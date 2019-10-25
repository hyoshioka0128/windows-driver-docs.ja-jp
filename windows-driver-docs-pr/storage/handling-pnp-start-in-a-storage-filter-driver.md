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
ms.openlocfilehash: 77838cae2f890a6b08e69eb7b1fc5020dec3542d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837553"
---
# <a name="handling-pnp-start-in-a-storage-filter-driver"></a>記憶域フィルター ドライバーでの PnP 開始の処理


## <span id="ddk_handling_pnp_start_in_a_storage_filter_driver_kg"></span><span id="DDK_HANDLING_PNP_START_IN_A_STORAGE_FILTER_DRIVER_KG"></span>


ストレージフィルタードライバー (SFD) は、デバイス固有の初期化を実行し、PnP マネージャーが開始要求 ([**irp\_MJ\_pnp**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)を\_使用して[*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンを呼び出したときに、そのデバイス拡張機能を設定し[ **\_\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)) を起動します。 SFD は、ストレージクラスドライバーとほぼ同じように開始要求を処理します。

ストレージクラスドライバーが開始要求を処理し、そのデバイス拡張機能を設定する方法の詳細については、「[ストレージクラスドライバー](storage-class-drivers.md)」を参照してください。 PnP 開始要求の処理に関する一般的な情報については、「[プラグアンドプレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)」を参照してください。

 

 




