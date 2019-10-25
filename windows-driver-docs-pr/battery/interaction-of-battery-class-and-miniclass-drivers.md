---
title: バッテリ クラス ドライバーとバッテリ ミニクラス ドライバーの相互作用
description: バッテリ クラス ドライバーとバッテリ ミニクラス ドライバーの相互作用
ms.assetid: bf35a034-1bb9-4106-aafe-7692d0ff92d0
keywords:
- バッテリ miniclass ドライバー WDK、バッテリクラスドライバーの相互作用
- バッテリクラスドライバー WDK、バッテリ miniclass ドライバーの相互作用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3724be94b0cce2a6ea7c3310f97d5e5333d1b924
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834002"
---
# <a name="interaction-of-battery-class-and-miniclass-drivers"></a>バッテリ クラス ドライバーとバッテリ ミニクラス ドライバーの相互作用


## <span id="ddk_interaction_of_battery_class_and_miniclass_drivers_dg"></span><span id="DDK_INTERACTION_OF_BATTERY_CLASS_AND_MINICLASS_DRIVERS_DG"></span>


バッテリクラスドライバーと miniclass ドライバーは、コンピューターのバッテリの使用を管理します。 次の図は、これらの2つのドライバーの相互作用を示しています。

![バッテリクラスと miniclass ドライバーの相互作用を示す図](images/battmini.png)

Miniclass ドライバーは、制御しているデバイスの主要な関数ドライバーです。 複合バッテリドライバーを介して電源マネージャーから Irp を受信し、バッテリクラスドライバーのサポートルーチンを呼び出して、デバイスを登録し、状態を報告し、システムで定義された特定のバッテリ Ioctl を処理します。

クラスドライバーは、すべての miniclass ドライバーから情報と状態を受け取り、複合バッテリドライバーを介して電源マネージャーに報告します。 バッテリ Ioctl への応答として、クラスドライバーは、特定のデバイス制御操作を実行するために、miniclass ドライバーの[バッテリ miniclass ドライバールーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/_battery/)(BatteryMini*Xxx*ルーチン) を呼び出します。 さらに、電源メーターなどのアプリケーションは、 [**IRP\_MJ\_デバイス\_制御**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)要求を miniclass ドライバーに送信して、特定のバッテリに関する情報を取得することもできます。

クラスドライバーは、温度や容量の変化など、可能性のあるバッテリ情報と状態のスーパーセットを処理するように設計されています。個々のバッテリは、これらのすべての条件を検出して報告する機能によって異なります。 各 miniclass ドライバーは、特定のバッテリの種類を管理するように設計する必要があり、バッテリがサポートしていない情報を要求されたときに、クラスドライバーに適切に応答する必要があります。

 

 




