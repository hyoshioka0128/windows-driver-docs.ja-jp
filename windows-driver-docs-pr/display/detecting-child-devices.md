---
title: 子デバイスの検出
description: 子デバイスの検出
ms.assetid: 36c0c4ef-7810-4e8a-b349-0b7c1f8c2f0c
keywords:
- ビデオのミニポート ドライバー WDK Windows 2000 では、子デバイス
- 子デバイス WDK ビデオ ミニポート、検出します。
- 子デバイス WDK のビデオのミニポートの検出
- HwVidGetVideoChildDescriptor
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e6978919b2dce9f3f36ca7c44f8735aa4626387
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348842"
---
# <a name="detecting-child-devices"></a>子デバイスの検出


## <span id="ddk_detecting_child_devices_gg"></span><span id="DDK_DETECTING_CHILD_DEVICES_GG"></span>


実装する必要があります[ *HwVidGetVideoChildDescriptor* ](https://msdn.microsoft.com/library/windows/hardware/ff567341)グラフィックス アダプターの子デバイスを検出することができる、プラグ アンド プレイ マネージャーは、ミニポート ドライバー。

既定では、 [ *HwVidGetVideoChildDescriptor* ](https://msdn.microsoft.com/library/windows/hardware/ff567341)まで、親デバイスが開始されている後に呼び出すことができません、 *HwVidGetVideoChildDescriptor*呼び出すことができませんまで後[ *HwVidFindAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff567332)が完了します。 設定することができます、いつでも発生する子列挙できますつまり、この既定をオーバーライドする、 **AllowEarlyEnumeration**のメンバー [**ビデオ\_HW\_の初期化。\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff570505)に**TRUE**します。

一部のデバイスは、システムまたは既存のハードウェアが、システムから切断されている場合、新しいハードウェアが接続されているときに、割り込みを生成します。 このような割り込みを処理するために、ミニポート ドライバーは、次の操作を行う必要があります。

-   DPC の実装 ([**HwVidDpcRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff567327)) を呼び出す[ **VideoPortEnumerateChildren**](https://msdn.microsoft.com/library/windows/hardware/ff570297)します。

-   割り込みハンドラーの実装 ([*HwVidInterrupt*](https://msdn.microsoft.com/library/windows/hardware/ff567349)) を呼び出す[ **VideoPortQueueDpc** ](https://msdn.microsoft.com/library/windows/hardware/ff570339)ときに、割り込み、DPC キューに入れ、デバイスに発生します。

[**VideoPortEnumerateChildren** ](https://msdn.microsoft.com/library/windows/hardware/ff570297)強制的によって、ミニポート ドライバーのアダプターの子のデバイスの再列挙[ *HwVidGetVideoChildDescriptor* ](https://msdn.microsoft.com/library/windows/hardware/ff567341)関数親デバイスの子のそれぞれに対して呼び出されます。 プラグ アンド プレイ マネージャーは、親デバイスとその子間のリレーションシップを適宜更新されます。

 

 





