---
title: バッテリのクラスと Miniclass ドライバーの相互作用
description: バッテリのクラスと Miniclass ドライバーの相互作用
ms.assetid: bf35a034-1bb9-4106-aafe-7692d0ff92d0
keywords:
- バッテリ miniclass ドライバー WDK、バッテリ クラス ドライバーの相互作用
- バッテリ クラス ドライバー WDK、バッテリ miniclass ドライバーの相互作用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e66ae9502d314715d099a6dd929a3d6cd7bb13d4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539234"
---
# <a name="interaction-of-battery-class-and-miniclass-drivers"></a>バッテリのクラスと Miniclass ドライバーの相互作用


## <span id="ddk_interaction_of_battery_class_and_miniclass_drivers_dg"></span><span id="DDK_INTERACTION_OF_BATTERY_CLASS_AND_MINICLASS_DRIVERS_DG"></span>


同時に、バッテリのクラス ドライバーと miniclass ドライバーは、バッテリのコンピューターの使用を管理します。 次の図は、これら 2 つのドライバーがやり取りする方法を示します。

![バッテリのクラスと miniclass ドライバーの相互作用を示す図](images/battmini.png)

Miniclass ドライバーは、制御デバイスの主な機能のドライバーです。 複合バッテリ ドライバーを通じて電源マネージャーから Irp を受信し、呼び出しは、状態をレポート、そのデバイスを登録して、あるシステム定義のバッテリ Ioctl を処理するために、バッテリのクラス ドライバーのルーチンをサポートします。

クラス ドライバーは、すべての miniclass ドライバーからの情報と状態を受信し、複合バッテリ ドライバーを通じて電源マネージャーに報告します。 バッテリの Ioctl に対応して、クラス ドライバー呼び出し[バッテリ miniclass ドライバー ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff536286)(BatteryMini*Xxx*ルーチン)、miniclass ドライバーには特定のデバイス管理操作を実行します。 また、電源メーターなどのアプリケーションを送信できます[ **IRP\_MJ\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550744) miniclass ドライバーに関する情報を取得する要求を特定のバッテリします。

クラスのドライバーが可能なバッテリに関する情報と、温度、容量、およびなどの変更のスーパー セットを処理するために設計されています個々 のバッテリを検出し、これらの条件をすべて報告機能によって異なります。 各 miniclass ドライバーでは、その特定のバッテリのタイプを管理するように設計する必要があり、バッテリがサポートされていないすべての情報を求められた場合、クラス ドライバーを適切に応答する必要があります。

 

 




