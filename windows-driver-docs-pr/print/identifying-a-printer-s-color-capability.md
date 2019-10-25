---
title: プリンターの色機能を特定する
description: プリンターの色機能を特定する
ms.assetid: 24abf76d-c0f9-440e-b825-8b39ea9ab807
keywords:
- プリンターインターフェイス DLL WDK、カラー機能がサポートされています
- 色の管理 WDK 印刷、機能の識別
- プリンターの色の機能を特定する
- プリンターの色の機能 WDK
- dmColor
- DC_COLORDEVICE
- DrvDeviceCapabilities
- モノクロ出力の WDK プリンター
- noncolor 出力 WDK プリンター
- グレースケール出力 WDK プリンター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41329f7d18464ff53dfe03ed402dac446a430aa4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837721"
---
# <a name="identifying-a-printers-color-capability"></a>プリンターの色機能を特定する





カラーと noncolor (モノクロまたはグレースケール) デバイスを区別するには、Windows 2000 以降の NT ベースのオペレーティングシステムバージョンで[**DrvDeviceCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdevicecapabilities)関数を呼び出し、DC\_colordevice 定数を呼び出しで渡します。 デバイスでカラーがサポートされている場合、この関数は1を返し、デバイスがモノクロまたはグレースケールの出力を生成する場合は0を返します。 すべてのプリンタードライバーで、DC\_COLORDEVICE 定数の**DrvDeviceCapabilities**の呼び出しをサポートすることをお勧めします。

[**DrvDeviceCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdevicecapabilities)関数を実装するには、ドライバーが非常に重要です。 そうしないと、次のような理由から、オペレーティングシステムが color デバイスと noncolor デバイスを区別することが難しくなります。

-   NUMCOLORS 定数が渡される**GetDeviceCaps**関数 (Windows SDK ドキュメントで説明されています) への呼び出しでは、通常、ほとんどの noncolor デバイスについては戻り値が2以下、カラーデバイスでは2以上になります。 オペレーティングシステムは、モノクロデバイスとグレースケールデバイスを区別できません。

-   [**Devmodew**](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)構造体の**dmcolor**メンバーの値は、デバイスが color または noncolor のどちらであるかを示す reliable indicator ではありません。 特定のプリンタードライバーは、色を作成できないデバイスでも、このメンバーを DMCOLOR\_色に設定します。

 

 




