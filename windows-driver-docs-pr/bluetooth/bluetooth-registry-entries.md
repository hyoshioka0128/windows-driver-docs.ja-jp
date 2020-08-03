---
title: Bluetooth レジストリ エントリ
description: Bluetooth レジストリ エントリ
ms.assetid: a4d2848d-cb3c-4413-b06f-fe4695448f6a
keywords:
- Bluetooth WDK、レジストリエントリ
- レジストリ WDK Bluetooth
- COD_Type サブキー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5298f160a02d80ff6d04a61ce374e8130d2fb09
ms.sourcegitcommit: 20a89aa2cb2c6385c2a49ebf78e5797c821d87ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2020
ms.locfileid: "87473724"
---
# <a name="bluetooth-registry-entries"></a>Bluetooth レジストリ エントリ

このセクションでは、Bluetooth ドライバースタックに適用されるデバイスクラス (CoD) レジストリサブキーとエントリについて説明します。

## <a name="cod-major-and-cod-type-values"></a>"COD Major" と "COD Type" の値

相手先ブランド供給の製造元 (Oem) は、 **cod の Major**および**cod の種類**の値を使用して、Bluetooth 対応の Windows デバイスのデバイスのクラスを示すことができます。 Bluetooth クラスのインストーラーによって、これらのレジストリ値に基づいてデバイスのクラスが設定されると、リモートデバイスはポータブルコンピューター、デスクトップコンピューター、電話などに接続しているかどうかを判断できます。

**Cod メジャー**と**cod 型**の値へのレジストリパスは次のとおりです。

HKEY \_ LOCAL \_ MACHINE \\ SYSTEM \\ CurrentControlSet \\ Services の \\ bthport \\ パラメーター

これらの値を設定すると、Bluetooth ラジオが取り付けられているかどうかに関係なく、システムのデバイスの Bluetooth クラスが変更されることに注意してください。 **Cod のメジャー**および**cod の種類**は、 `DWORD` [Bluetooth SIG の割り当て番号](https://www.bluetooth.com/specifications/assigned-numbers/baseband/)のデバイスフィールド値のクラスに対して定義されている値に設定できます。

Bluetooth プロファイルドライバーである BthPort.sys は、 **Cod メジャー**および**cod 型**の値を読み取って、デバイスの照会にどのように応答するかを決定します。 これらの値は、 `COD_MAJOR_XXX` デバイスのクラスとビットにのみ影響し `COD_XXX_MINOR_XXX` ます。 ビットは、 `COD_SERVICE_XXX` このレジストリエントリの影響を受けません。

Cod の**Major**および**cod 型**の値が設定されていない場合、または無効な値に設定されている場合は、Bluetooth クラスのインストーラーによって、これらの値がそれぞれとに設定され `COD_MAJOR_COMPUTER` `COD_COMPUTER_MINOR_DESKTOP` ます。

## <a name="scanning-parameterization-settings"></a>パラメーター化の設定をスキャンしています

プロファイルドライバーは、特定のデバイスシナリオの特定のニーズに合わせて調整するために、プロファイルドライバーの INF ファイル内のデバイスのスキャンパラメーター設定を指定できます。

次に示す1つ以上のスキャンパラメーターを AddReg ディレクティブに指定すると、既定のシステムスキャンパラメーターを上書きできます。 このディレクティブの使用方法の詳細については、「 [INF AddReg ディレクティブ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)」を参照してください。

| 値名                | 種類          | Min Value (最小値) | Max Value (最大値)                                                                      |
|----|----|----|----|
| HighDutyCycleScanWindow   | DWORD 0x10001 | 0x0004    | 0x4000. は HighDutyCycleScanInterval パラメーターと同じか、それより小さい値にする必要があります |
| HighDutyCycleScanInterval | DWORD 0x10001 | 0x0004    | 0x4000                                                                         |
| LowDutyCycleScanWindow    | DWORD 0x10001 | 0x0004    | 0x4000. は LowDutyCycleScanInterval パラメーターよりも小さくする必要があります           |
| LowDutyCycleScanInterval  | DWORD 0x10001 | 0x0004    | 0x4000                                                                         |
| LinkSupervisionTimeout    | DWORD 0x10001 | 0x000A    | 0x0C80                                                                         |
| ConnectionLatency         | DWORD 0x10001 | 0x0000    | 0x01F4                                                                         |
| ConnectionIntervalMin     | DWORD 0x10001 | 0x0006    | 0x0C80。 は、ConnectionIntervalMax 以下でなければなりません                     |
| ConnectionIntervalMax     | DWORD 0x10001 | 0x0006    | 0x0C80                                                                         |

>[!NOTE]
>スキャンパラメーターを変更すると、Bluetooth スタックのパフォーマンスにグローバルな影響が生じます。 プログラムによってパラメーターのスキャンを変更することはできません。 低負荷サイクルのスキャンパラメーターを使用すると、他の Bluetooth 低エネルギー接続で使用可能な帯域幅に悪影響を与えるだけでなく、Bluetooth BR/EDR 接続にも悪影響を及ぼす可能性があります。
