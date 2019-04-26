---
title: 16550 UART インターフェイス用に PnP シリアル デバイスを構成する
description: 16550 UART と互換性のあるインターフェイスを必要とするプラグ アンド プレイ シリアル デバイスの構成
ms.assetid: b99259bd-7573-4f71-9ab5-b263eed41288
keywords:
- プラグ アンド プレイ シリアル デバイス WDK
- シリアル デバイス WDK、プラグ アンド プレイ
- ユニバーサル非同期の受信側の送信機 WDK シリアル デバイス
- UART WDK シリアル デバイス
- 16550 UART と互換性のあるインターフェイス WDK シリアル デバイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d33022330c634889e371ed428c898d702098eff
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344984"
---
# <a name="configuration-of-plug-and-play-serial-device-that-requires-a-16550-uart-compatible-interface"></a>16550 UART と互換性のあるインターフェイスを必要とするプラグ アンド プレイ シリアル デバイスの構成





このセクションでは、シリアル デバイスに使用されるハードウェア、ドライバー、およびデバイス スタックの一般的な構成をについて説明します。

-   プラグ アンド プレイをサポートします。

-   16550 UART と互換性のあるインターフェイスが必要です。

-   Rs-232 ポートに接続されていません。

たとえば、モデムの PCMCIA カードです。

次の図は、サンプルのトースター デバイスと 16550 UART と互換性のあるインターフェイスを必要とするサンプル blender デバイスに対する一般的な構成を示します。

![左側の図: pcmcia カードのプラグ アンド プレイ トースター デバイスのハードウェア構成。 右側の図: ドライバーや pcmcia カードのプラグ アンド プレイ トースター デバイスのデバイス履歴の構成](images/ser3.png)

これらの構成では、トースター デバイスは PCMCIA バス上の子デバイスです。 PCMCIA バス ドライバーは、PCMCIA カードを列挙したときにトースター デバイス用の PDO を作成します。 トースター デバイスの INF ファイルでは、低レベル デバイス フィルター ドライバーとしてシリアルを指定します。 シリアルは、ハードウェア デバイスに 16550 UART と互換性のあるインターフェイスを提供します。 トースター ドライバーでは、作成し、トースター デバイス スタックに FDO をアタッチします。

 

 




