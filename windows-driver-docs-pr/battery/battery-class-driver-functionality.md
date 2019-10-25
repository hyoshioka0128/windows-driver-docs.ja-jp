---
title: バッテリ クラス ドライバーの機能
description: バッテリ クラス ドライバーの機能
ms.assetid: cd7536d9-bcf1-4674-8ebf-af2b888a0f0a
keywords:
- バッテリクラスドライバー WDK、機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f7b110d7992ab71b79cb3d354715dce38eb2ac1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829919"
---
# <a name="battery-class-driver-functionality"></a>バッテリ クラス ドライバーの機能


## <span id="ddk_battery_class_driver_functionality_dg"></span><span id="DDK_BATTERY_CLASS_DRIVER_FUNCTIONALITY_DG"></span>


カーネルモードバッテリクラスドライバー battc は、デバイスに依存しないバッテリサポートを提供し、すべてのデバイス固有のバッテリ miniclass ドライバーで使用するためのサポートルーチンをエクスポートします。

バッテリクラスドライバーは、miniclass ドライバーに関して次のタスクを実行します。

-   Miniclass ドライバーの初期化の大部分を実行します。たとえば、miniclass ドライバーのクラスデータのシステムリソースと領域の割り当てを含みます。

-   バッテリクラス Ioctl を指定するデバイスコントロールの Irp ([**irp\_MJ\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)) を処理します。 (これらの Ioctl の詳細については、Microsoft Windows SDK を参照してください)。

-   バッテリデバイスへの要求をシリアル化する

-   オペレーティングシステムの DC 電源ポリシーを管理する

-   Miniclass ドライバーがアンロードされた場合のシステムリソースの解放

-   特定の標準バッテリの WMI クラスの処理

バッテリクラスドライバーがバッテリ Miniclass ドライバーにエクスポートするルーチンの説明については、「[バッテリ Miniclass ドライバールーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/_battery/)」を参照してください。

 

 




