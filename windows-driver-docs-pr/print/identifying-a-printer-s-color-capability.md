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
ms.openlocfilehash: 85344b81de44a0e82d1c9e4b5f80e96544b8c307
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380837"
---
# <a name="identifying-a-printers-color-capability"></a>プリンターの色機能を特定する





色とモノクロ (モノクロまたはグレースケール) デバイス、Windows 2000、および後で NT ベースのオペレーティング システムのバージョンの呼び出しを区別する、 [ **DrvDeviceCapabilities** ](https://msdn.microsoft.com/library/windows/hardware/ff548539) DC を渡す関数\_呼び出しで COLORDEVICE 定数。 この関数は、デバイスは、モノクロまたはグレースケールの出力を生成した場合の色、および 0 をデバイスがサポートする場合に、1 を返します。 すべてのプリンター ドライバーがへの呼び出しをサポートすることをお勧め**DrvDeviceCapabilities** 、DC の\_COLORDEVICE 定数。

実装するドライバーを非常に重要ですが、 [ **DrvDeviceCapabilities** ](https://msdn.microsoft.com/library/windows/hardware/ff548539)関数。 色とモノクロの間の次の理由から、デバイスを区別するために、オペレーティング システムの場合はそれ以外の場合です。

-   呼び出し、**調べるため**関数 (Windows SDK のドキュメントで説明)、NUMCOLORS 定数が渡されます、通常は戻り値の結果値のほとんどのモノクロ デバイスとの 2 より大きい 2 未満デバイスの色。 オペレーティング システムは、モノクロおよびグレースケールのデバイスを区別することができます。

-   値、 **dmColor**のメンバー、 [ **DEVMODEW** ](https://msdn.microsoft.com/library/windows/hardware/ff552837)構造がないかどうか、デバイスは、カラーかモノクロ デバイスの信頼性の高いインジケーター。 特定のプリンター ドライバーでは、このメンバーを設定する DMCOLOR\_対応の色を生成していないデバイスの場合でも色。

 

 




