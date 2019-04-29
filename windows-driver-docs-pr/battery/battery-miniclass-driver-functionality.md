---
title: バッテリ ミニクラス ドライバーの機能
description: バッテリ ミニクラス ドライバーの機能
ms.assetid: f8da63fd-0bf9-4085-88c2-022c4ddc7caa
keywords:
- バッテリ miniclass ドライバー WDK、機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f4a9309a6835b02d33a79798788098c38bddf07e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335249"
---
# <a name="battery-miniclass-driver-functionality"></a>バッテリ ミニクラス ドライバーの機能


## <span id="ddk_battery_miniclass_driver_functionality_dg"></span><span id="DDK_BATTERY_MINICLASS_DRIVER_FUNCTIONALITY_DG"></span>


バッテリ miniclass ドライバーは、次の場合です。

-   そのデバイス用に FDO の作成と関連付けられているデバイスの拡張機能にデバイスに固有の情報を格納します。

-   割り当てとバッテリのタグの現在のバッテリを維持

-   バッテリ容量、料金、および電源の状態を追跡します。

-   バッテリの状態情報用のクラス ドライバーからの要求に応答

-   バッテリの電力状態が変更されたときにバッテリ クラス ドライバーへの通知

-   充電中か、要求されたときに特定のバッテリが放電しています

バッテリ miniclass ドライバーは」の説明に従って、Ioctl の処理などの他の操作のバッテリ クラス ドライバーのサポート ルーチンを呼び出す[バッテリ クラス ドライバー機能](battery-class-driver-functionality.md)します。

すべてのバッテリ miniclass ドライバーのセットを提供する[BatteryMini*Xxx* ](https://msdn.microsoft.com/library/windows/hardware/ff536286)ルーチン。 バッテリ クラス ドライバーは、miniclass ドライバーがデバイスに固有のタスクを実行することを要求するこれらのルーチンを呼び出します。 さらに、miniclass ドライバーする必要がありますが、その他のルーチン」の説明に従って[提供するために必要なバッテリ Miniclass ドライバー機能](supplying-required-battery-miniclass-driver-functionality.md)します。

 

 




