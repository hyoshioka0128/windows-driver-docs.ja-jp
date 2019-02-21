---
title: 書き込みバッテリ Miniclass ドライバー
description: 書き込みバッテリ Miniclass ドライバー
ms.assetid: 4135af1a-1448-46ad-af6f-26ce8aee6b1d
keywords:
- バッテリ miniclass ドライバー WDK
- バッテリ miniclass ドライバーの記述について miniclass ドライバー WDK、バッテリ
- デバイスに依存しないバッテリ サポート WDK
- 特定のデバイスのバッテリ サポート WDK
- バッテリ クラス ドライバー WDK
- バッテリ クラス ドライバーに関するクラス ドライバー WDK、バッテリ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc25453bdb285ae71edd8fd64d59296ccc9115a2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558824"
---
# <a name="writing-battery-miniclass-drivers"></a>書き込みバッテリ Miniclass ドライバー


## <span id="ddk_writing_battery_miniclass_drivers_dg"></span><span id="DDK_WRITING_BATTERY_MINICLASS_DRIVERS_DG"></span>


ドライバーのペアが通常、バッテリには: Microsoft が提供する汎用的なバッテリ クラス ドライバーとバッテリの個々 の型専用に作成された miniclass ドライバー。

クラス ドライバーは、システムのバッテリの全体的な機能を定義し、電源マネージャーと対話します。

Miniclass ドライバーでは、デバイス固有の関数を追加して、バッテリの削除の容量と料金の追跡などを処理します。 Miniclass ドライバーでは、クラス ドライバーは制御デバイスに関する情報を取得するために呼び出すルーチンをエクスポートします。

バッテリ miniclass ドライバーの作成方法については、次のように構成されています。

[システム バッテリの管理の概要](overview-of-system-battery-management.md)

[バッテリのクラスと Miniclass ドライバーの相互作用](interaction-of-battery-class-and-miniclass-drivers.md)

[バッテリ Miniclass ドライバー機能に必要な指定](supplying-required-battery-miniclass-driver-functionality.md)

[バッテリ Miniclass ドライバーの DriverEntry ルーチン](driverentry-routine-of-a-battery-miniclass-driver.md)

[バッテリ Miniclass ドライバーの AddDevice ルーチン](adddevice-routine-of-a-battery-miniclass-driver.md)

[バッテリ Miniclass ドライバーの DispatchDeviceControl ルーチン](dispatchdevicecontrol-routine-of-a-battery-miniclass-driver.md)

[バッテリ Miniclass ドライバーの DispatchSystemControl ルーチン](dispatchsystemcontrol-routine-of-a-battery-miniclass-driver.md)

[バッテリ クラス ドライバーのクエリに応答してください。](responding-to-battery-class-driver-queries.md)

[バッテリのデバイスの通知を提供します。](supplying-battery-device-notification.md)

[バッテリ Miniclass ドライバーをアンロード ルーチン](unload-routine-of-a-battery-miniclass-driver.md)

[バッテリのドライバーをインストールします。](installing-a-battery-driver.md)

 

 




