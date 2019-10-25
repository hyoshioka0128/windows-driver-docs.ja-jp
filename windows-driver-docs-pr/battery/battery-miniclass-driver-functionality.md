---
title: バッテリ ミニクラス ドライバーの機能
description: バッテリ ミニクラス ドライバーの機能
ms.assetid: f8da63fd-0bf9-4085-88c2-022c4ddc7caa
keywords:
- バッテリ miniclass ドライバー WDK、機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7081f17614880fc617f0c5a8e44fd5dac4713668
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832223"
---
# <a name="battery-miniclass-driver-functionality"></a>バッテリ ミニクラス ドライバーの機能


## <span id="ddk_battery_miniclass_driver_functionality_dg"></span><span id="DDK_BATTERY_MINICLASS_DRIVER_FUNCTIONALITY_DG"></span>


バッテリ miniclass ドライバーは、次のことを担当します。

-   デバイスの FDO を作成し、関連付けられているデバイス拡張機能にデバイス固有の情報を格納する

-   現在のバッテリのバッテリタグの割り当てと維持

-   バッテリの容量、料金、電源の状態を追跡する

-   クラスドライバーからのバッテリ状態情報の要求への応答

-   バッテリの電源状態が変化したときにバッテリクラスドライバーに通知する

-   要求時に特定のバッテリを充電または放電する

バッテリ miniclass ドライバーは、「[バッテリクラスドライバーの機能](battery-class-driver-functionality.md)」で説明されているように、ioctl の処理など、他の操作に対してバッテリクラスドライバーのサポートルーチンを呼び出します。

すべてのバッテリ miniclass ドライバーには、一連の[BatteryMini*Xxx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/_battery/)ルーチンが用意されています。 バッテリクラスドライバーは、これらのルーチンを呼び出して、miniclass ドライバーがデバイス固有のタスクを実行するように要求します。 また、miniclass ドライバーには、「[必要なバッテリ Miniclass ドライバー機能の提供](supplying-required-battery-miniclass-driver-functionality.md)」で説明されているように、他のルーチンが必要です。

 

 




