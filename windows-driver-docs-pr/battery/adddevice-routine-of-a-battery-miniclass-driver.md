---
title: バッテリ ミニクラス ドライバーの AddDevice ルーチン
description: バッテリ ミニクラス ドライバーの AddDevice ルーチン
ms.assetid: 1b34e223-e238-4547-bd44-754be2e6749c
keywords:
- AddDevice ルーチン WDK バッテリ
- バッテリ miniclass ドライバー WDK、ルーチン
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 047409777394f18b83f1484ddd107c53de627969
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335415"
---
# <a name="adddevice-routine-of-a-battery-miniclass-driver"></a>バッテリ ミニクラス ドライバーの AddDevice ルーチン


## <span id="ddk_adddevice_routine_of_battery_miniclass_driver_dg"></span><span id="DDK_ADDDEVICE_ROUTINE_OF_BATTERY_MINICLASS_DRIVER_DG"></span>


すべてのバッテリ miniclass ドライバーが必要、 [ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)ルーチンで、バッテリ固有の状態を初期化します。 PnP マネージャー呼び出し、 *AddDevice*この miniclass ドライバーによって制御される各バッテリのデバイスの日常的な。

PnP の必要なタスクだけでなく*AddDevice* 、ルーチン、 *AddDevice*バッテリ miniclass ドライバーのルーチンでは、次を行う必要がありますも。

1.  バッテリの FDO を作成し、コント ローラー デバイス スタックを FDO を関連付けます。

2.  初期化、 [**バッテリ\_ミニポート\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff536287)構造と呼び出し[ **BatteryClassInitializeDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff536266)バッテリ クラス ドライバーを使用した miniclass ドライバーを登録します。

3.  他のデバイスに必要な初期化を実行します。

 

 




