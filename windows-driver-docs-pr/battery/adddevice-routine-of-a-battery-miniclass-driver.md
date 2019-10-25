---
title: バッテリ ミニクラス ドライバーの AddDevice ルーチン
description: バッテリ ミニクラス ドライバーの AddDevice ルーチン
ms.assetid: 1b34e223-e238-4547-bd44-754be2e6749c
keywords:
- AddDevice ルーチン WDK バッテリ
- バッテリ miniclass ドライバー WDK、ルーチン
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ddbfc3ea8a22318cf78316a91e2d3574f47742b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832229"
---
# <a name="adddevice-routine-of-a-battery-miniclass-driver"></a>バッテリ ミニクラス ドライバーの AddDevice ルーチン


## <span id="ddk_adddevice_routine_of_battery_miniclass_driver_dg"></span><span id="DDK_ADDDEVICE_ROUTINE_OF_BATTERY_MINICLASS_DRIVER_DG"></span>


すべてのバッテリ miniclass ドライバーには、バッテリ固有の状態を初期化する[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンが必要です。 PnP マネージャーは、この miniclass ドライバーによって制御される各バッテリデバイスの*AddDevice*ルーチンを呼び出します。

PnP *AddDevice*ルーチンに必要なタスクに加えて、バッテリ miniclass ドライバーの*AddDevice*ルーチンでは、次の操作も行う必要があります。

1.  バッテリの FDO を作成し、コントローラーのデバイススタックに FDO をアタッチします。

2.  [**バッテリ\_ミニポート\_情報**](https://docs.microsoft.com/windows/desktop/api/batclass/ns-batclass-battery_miniport_info)構造体を初期化し、 [**BatteryClassInitializeDevice**](https://docs.microsoft.com/windows/desktop/api/batclass/nf-batclass-batteryclassinitializedevice)を呼び出して、miniclass ドライバーをバッテリクラスドライバーに登録します。

3.  デバイスに必要なその他の初期化を実行します。

 

 




