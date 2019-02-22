---
title: 16550 UART インターフェイスでの PnP 多機能シリアル デバイスを構成します。
description: 16550 UART と互換性のあるインターフェイスを必要とする多機能デバイスのプラグ アンド プレイ シリアル デバイスの構成
ms.assetid: 63588ac9-4c87-421d-8da3-3e950cbd466c
keywords:
- プラグ アンド プレイ シリアル デバイス WDK
- シリアル デバイス WDK、プラグ アンド プレイ
- ユニバーサル非同期の受信側の送信機 WDK シリアル デバイス
- UART WDK シリアル デバイス
- 16550 UART と互換性のあるインターフェイス WDK シリアル デバイス
- 多機能デバイス
- 多機能デバイス WDK シリアル デバイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0dce95ec1d57f8d591543b321a28a04b89402e84
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553224"
---
# <a name="configuration-of-plug-and-play-serial-device-on-a-multifunction-device-that-requires-a-16550-uart-compatible-interface"></a>16550 UART と互換性のあるインターフェイスを必要とする多機能デバイスのプラグ アンド プレイ シリアル デバイスの構成





このセクションは、多機能シリアル デバイスのハードウェア、ドライバー、およびデバイスのスタックの構成を記述します。

-   プラグ アンド プレイをサポートします。

-   16550 UART と互換性のあるインターフェイスが必要です。

-   Rs-232 ポートに接続されていません。

具体的な例は、モデムと LAN アダプターを持つ PCMCIA カードです。

次の図は、サンプルのトースター デバイスと 16550 UART と互換性のあるインターフェイスを必要とするサンプル blender デバイスに対する一般的な構成を示しています。

![図に示すハードウェアとドライバー-と-デバイスのスタックの構成とトースターおよび blender 多機能 pcmcia カードでは、トースターに関する](images/ser4.png)

これらの構成では、トースター デバイスは、多機能のデバイスでは、子デバイスと多機能デバイス、PCMCIA バス上の子デバイス。

INF ファイルとトースター デバイス用のインストーラーは、トースター デバイス 16550 UART と互換性のあるインターフェイスを提供する低レベル デバイス フィルター ドライバーとしてシリアル ドライバーをインストールします。 トースター ドライバーを作成し、接続 FDO シリアル ドライバーのフィルター操作を行います。

 

 




