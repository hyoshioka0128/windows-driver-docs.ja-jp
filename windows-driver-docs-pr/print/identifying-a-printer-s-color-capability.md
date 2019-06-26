---
title: プリンターの色機能を特定する
description: プリンターの色機能を特定する
ms.assetid: 24abf76d-c0f9-440e-b825-8b39ea9ab807
keywords:
- プリンター インターフェイス DLL の WDK、サポートされている色の機能
- WDK の印刷、機能の特定の色の管理
- プリンターの色の機能を識別します。
- プリンターのカラー機能 WDK
- dmColor
- DC_COLORDEVICE
- DrvDeviceCapabilities
- モノクロ出力 WDK プリンター
- モノクロ印刷の WDK プリンター
- グレースケール印刷 WDK のプリンター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f50078222e1b210934e8d803adf0011c80dd8686
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382563"
---
# <a name="identifying-a-printers-color-capability"></a>プリンターの色機能を特定する





色とモノクロ (モノクロまたはグレースケール) デバイス、Windows 2000、および後で NT ベースのオペレーティング システムのバージョンの呼び出しを区別する、 [ **DrvDeviceCapabilities** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvdevicecapabilities) DC を渡す関数\_呼び出しで COLORDEVICE 定数。 この関数は、デバイスは、モノクロまたはグレースケールの出力を生成した場合の色、および 0 をデバイスがサポートする場合に、1 を返します。 すべてのプリンター ドライバーがへの呼び出しをサポートすることをお勧め**DrvDeviceCapabilities** 、DC の\_COLORDEVICE 定数。

実装するドライバーを非常に重要ですが、 [ **DrvDeviceCapabilities** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvdevicecapabilities)関数。 色とモノクロの間の次の理由から、デバイスを区別するために、オペレーティング システムの場合はそれ以外の場合です。

-   呼び出し、**調べるため**関数 (Windows SDK のドキュメントで説明)、NUMCOLORS 定数が渡されます、通常は戻り値の結果値のほとんどのモノクロ デバイスとの 2 より大きい 2 未満デバイスの色。 オペレーティング システムは、モノクロおよびグレースケールのデバイスを区別することができます。

-   値、 **dmColor**のメンバー、 [ **DEVMODEW** ](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)構造がないかどうか、デバイスは、カラーかモノクロ デバイスの信頼性の高いインジケーター。 特定のプリンター ドライバーでは、このメンバーを設定する DMCOLOR\_対応の色を生成していないデバイスの場合でも色。

 

 




