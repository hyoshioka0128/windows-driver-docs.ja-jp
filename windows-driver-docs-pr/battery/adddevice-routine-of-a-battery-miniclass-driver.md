---
title: バッテリ ミニクラス ドライバーの AddDevice ルーチン
description: バッテリ ミニクラス ドライバーの AddDevice ルーチン
ms.assetid: 1b34e223-e238-4547-bd44-754be2e6749c
keywords:
- AddDevice ルーチン WDK バッテリ
- バッテリ miniclass ドライバー WDK、ルーチン
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ea8bc8c250f38ec144e8484d84b5ca13e95bf5a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354081"
---
# <a name="adddevice-routine-of-a-battery-miniclass-driver"></a>バッテリ ミニクラス ドライバーの AddDevice ルーチン


## <span id="ddk_adddevice_routine_of_battery_miniclass_driver_dg"></span><span id="DDK_ADDDEVICE_ROUTINE_OF_BATTERY_MINICLASS_DRIVER_DG"></span>


すべてのバッテリ miniclass ドライバーが必要、 [ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)ルーチンで、バッテリ固有の状態を初期化します。 PnP マネージャー呼び出し、 *AddDevice*この miniclass ドライバーによって制御される各バッテリのデバイスの日常的な。

PnP の必要なタスクだけでなく*AddDevice* 、ルーチン、 *AddDevice*バッテリ miniclass ドライバーのルーチンでは、次を行う必要がありますも。

1.  バッテリの FDO を作成し、コント ローラー デバイス スタックを FDO を関連付けます。

2.  初期化、 [**バッテリ\_ミニポート\_情報**](https://docs.microsoft.com/windows/desktop/api/batclass/ns-batclass-battery_miniport_info)構造と呼び出し[ **BatteryClassInitializeDevice** ](https://docs.microsoft.com/windows/desktop/api/batclass/nf-batclass-batteryclassinitializedevice)バッテリ クラス ドライバーを使用した miniclass ドライバーを登録します。

3.  他のデバイスに必要な初期化を実行します。

 

 




