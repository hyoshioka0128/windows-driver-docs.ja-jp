---
title: Bluetooth レジストリ エントリ
description: Bluetooth レジストリ エントリ
ms.assetid: a4d2848d-cb3c-4413-b06f-fe4695448f6a
keywords:
- Bluetooth の WDK、レジストリ エントリ
- レジストリ WDK Bluetooth
- COD_Type サブキー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08e9f13edd8d2e5e831f46f91baa135ad086c6e1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364662"
---
# <a name="bluetooth-registry-entries"></a>Bluetooth レジストリ エントリ


このセクションでは、クラスからのデバイス (CoD) レジストリ サブキーと、Bluetooth ドライバー スタックに適用されるエントリについて説明します。

### <a name="span-idcodtypesubkeyspanspan-idcodtypesubkeyspancod-major-and-cod-type-values"></a><span id="cod_type_subkey"></span><span id="COD_TYPE_SUBKEY"></span>「COD メジャー」と"COD Type"値

供給元 (Oem) が使用できる、 **COD メジャー**と**COD 型**を Bluetooth 対応の Windows デバイスのデバイス クラスを示す値。 Bluetooth クラスのインストーラーは、これらのレジストリ値に基づいて、デバイスのクラスを設定、リモート デバイスがポータブル コンピューター、デスクトップ コンピューター、電話を接続しているかどうかを判断することができます。

レジストリのパス、 **COD メジャー**と**COD 型**値は。

HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\サービス\\BTHPORT\\パラメーター

これらの値の設定、Bluetooth 無線接続に関係なく、システムでは、デバイスの Bluetooth クラスが変わることに注意してください。 設定することができます、 **COD メジャー**と**COD 型**に`DWORD`値クラスのデバイスに対して定義されているフィールドの値、 [Bluetooth SIG Assigned Numbers](https://www.bluetooth.com/specifications/assigned-numbers/baseband/)します。

Bluetooth のプロファイル ドライバー BthPort.sys、読み取り、 **COD メジャー**と**COD 型**の値を調べて、デバイスの照会に反応する必要があります。 これらの値に影響するのみ、`COD_MAJOR_XXX`と`COD_XXX_MINOR_XXX`クラスのデバイスのビット。 `COD_SERVICE_XXX`ビットがこのレジストリ エントリを受けません。

場合、 **COD メジャー**と**COD 型**Bluetooth クラスのインストーラーにこれらの値を設定する値が設定されていないか、無効な値に設定されて、`COD_MAJOR_COMPUTER`と`COD_COMPUTER_MINOR_DESKTOP`、それぞれします。

### <a name="span-idscanningparameterizationsettingsspanspan-idscanningparameterizationsettingsspanspan-idscanningparameterizationsettingsspanscanning-parameterization-settings"></a><span id="Scanning_Parameterization_Settings"></span><span id="scanning_parameterization_settings"></span><span id="SCANNING_PARAMETERIZATION_SETTINGS"></span>パラメーター化の設定をスキャンします。

プロファイルのドライバーでは、特定のデバイスのシナリオの特定のニーズに合わせてカスタマイズする、プロファイル ドライバーの INF ファイルで、デバイスのスキャンのパラメーター設定を指定できます。

いずれかを指定してパラメーターをスキャンする既定のシステムをオーバーライドするまたは AddReg ディレクティブに下記の次のスキャンのパラメーター。 このディレクティブを使用する方法の詳細についてで参照できる[INF AddReg ディレクティブ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)します。

|                           |               |           |                                                                                |
|---------------------------|---------------|-----------|--------------------------------------------------------------------------------|
| ［値の名前］                | 種類          | 最小値 | 最大値                                                                      |
| HighDutyCycleScanWindow   | DWORD 0x10001 | 0x0004    | 0x4000 です。 同じか HighDutyCycleScanInterval パラメーター未満にする必要があります。 |
| HighDutyCycleScanInterval | DWORD 0x10001 | 0x0004    | 0x4000                                                                         |
| LowDutyCycleScanWindow    | DWORD 0x10001 | 0x0004    | 0x4000 です。 LowDutyCycleScanInterval パラメーターよりも小さくする必要があります。           |
| LowDutyCycleScanInterval  | DWORD 0x10001 | 0x0004    | 0x4000                                                                         |
| LinkSupervisionTimeout    | DWORD 0x10001 | 0x000A    | 0x0C80                                                                         |
| ConnectionLatency         | DWORD 0x10001 | 0x0000    | 0x01F4                                                                         |
| ConnectionIntervalMin     | DWORD 0x10001 | 0x0006    | 0x0C80 します。 ConnectionIntervalMax 以下にする必要があります。                     |
| ConnectionIntervalMax     | DWORD 0x10001 | 0x0006    | 0x0C80                                                                         |

 

**注**  スキャン パラメーター変更により、Bluetooth スタックのパフォーマンスに、グローバルに影響します。 パラメーターをプログラムによってスキャンに変更を加えることは許可されていません。 低負荷サイクルを使用してスキャンの頻度が高すぎたパラメーターはありませんしか他の Bluetooth 低エネルギー接続で Bluetooth BR/EDR 接続に対しても使用可能な帯域幅に影響を及ぼす。

 

 

 





