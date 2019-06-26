---
title: バッテリ クラス ドライバーの機能
description: バッテリ クラス ドライバーの機能
ms.assetid: cd7536d9-bcf1-4674-8ebf-af2b888a0f0a
keywords:
- バッテリ クラス ドライバー WDK、機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b724319a72a710bfb3efe7e98bae3620fabf517
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364771"
---
# <a name="battery-class-driver-functionality"></a>バッテリ クラス ドライバーの機能


## <span id="ddk_battery_class_driver_functionality_dg"></span><span id="DDK_BATTERY_CLASS_DRIVER_FUNCTIONALITY_DG"></span>


カーネル モードのバッテリ クラス ドライバーのため、battc.sys、デバイスに依存しないバッテリのサポートを提供して、エクスポートは、すべてのデバイスに固有のバッテリ miniclass ドライバーによる使用のルーチンをサポートします。

バッテリ クラス ドライバー miniclass ドライバーの次のタスクを行います。

-   Miniclass ドライバーの初期化、miniclass ドライバーのクラスのデータ用のシステム リソースと容量の割り当てなどの大きな部分を実行します。

-   デバイスの制御 Irp の処理 ([**IRP\_MJ\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)) バッテリ クラス Ioctl を指定します。 (これらの Ioctl については、Microsoft Windows SDK を参照してください)。

-   バッテリのデバイスへの要求をシリアル化します。

-   オペレーティング システムの DC 電源ポリシーの管理

-   Miniclass ドライバーが読み込まれている場合は、システム リソースを解放します。

-   特定の標準のバッテリ WMI クラスの処理

参照してください[バッテリ Miniclass ドライバー ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_battery/)バッテリ miniclass ドライバーにバッテリ クラス ドライバーをエクスポートするルーチンの説明についてはします。

 

 




