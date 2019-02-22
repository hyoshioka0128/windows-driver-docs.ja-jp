---
title: Bluetooth に関する FAQ
description: この FAQ のセクションでは、Windows ファミリのオペレーティング システムの Bluetooth ワイヤレス技術のサポートについての情報を提供します。
ms.assetid: 529DD4A2-4E4B-47F4-BD65-BE89EA21E217
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c18d2e9d8420c09dfb2bf3d8cc890dd77a59454c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558729"
---
# <a name="bluetooth-faq"></a>Bluetooth に関する FAQ


この FAQ のセクションでは、Windows ファミリのオペレーティング システムの Bluetooth ワイヤレス技術のサポートについての情報を提供します。 主に初心者、ハードウェアとソフトウェアの開発者向けの Windows とアドレスに関する Bluetooth エコシステムには、独立系ハードウェア ベンダー (Ihv) するためのものです。

その他のよく寄せられる質問は、次のトピックに配置されます。

[Windows 10 で Bluetooth のバージョンとプロファイルのサポート](general-bluetooth-support-in-windows.md)
[Bluetooth バージョンおよびプロファイルを Windows の以前のバージョンでサポート](bluetooth-support-in-previous-windows-versions.md)
[Bluetooth ホスト ラジオ サポート](bluetooth-host-radio-support.md) 
 [Bluetooth ユーザー インターフェイス](bluetooth-user-interface.md)
[Bluetooth 証明](bluetooth-certification.md)
[付録 A](bluetooth-faq--appendix-a.md) 
[付録 B](bluetooth-faq--appendix-b.md)
## <a name="span-idhowmanybluetoothradioscanwindowssupportspanspan-idhowmanybluetoothradioscanwindowssupportspanspan-idhowmanybluetoothradioscanwindowssupportspanhow-many-bluetooth-radios-can-windows-support"></a><span id="How_many_Bluetooth_radios_can_Windows_support_"></span><span id="how_many_bluetooth_radios_can_windows_support_"></span><span id="HOW_MANY_BLUETOOTH_RADIOS_CAN_WINDOWS_SUPPORT_"></span>Bluetooth ラジオの数は Windows をサポートしますか?


Windows で Bluetooth スタックには、1 つだけの Bluetooth 無線がサポートされています。 このオプションは、Bluetooth 仕様と最新の Windows ハードウェア認定プログラム要件に準拠する必要があります。

## <a name="span-idhowcanbluetoothandwi-firadioscoexisteffectivelyspanspan-idhowcanbluetoothandwi-firadioscoexisteffectivelyspanspan-idhowcanbluetoothandwi-firadioscoexisteffectivelyspanhow-can-bluetooth-and-wi-fi-radios-coexist-effectively"></a><span id="How_can_Bluetooth_and_Wi-Fi_radios_coexist_effectively_"></span><span id="how_can_bluetooth_and_wi-fi_radios_coexist_effectively_"></span><span id="HOW_CAN_BLUETOOTH_AND_WI-FI_RADIOS_COEXIST_EFFECTIVELY_"></span>どのし、Wi-fi、Bluetooth 無線共存させることは効果的にでしょうか。


Wi-fi と Bluetooth の両方のラジオは、同じ周波数を使用しようと、一時的にように 2.4 GHz の周波数の範囲で動作します。 Bluetooth ワイヤレス技術を使用する手法をホッピング頻度では、このような競合を防止、完全な接続の損失が発生しますが、両方の無線の転送率を減らすことができます。

Bluetooth の仕様のバージョン 2.0 では、AFH をサポートします。 AFH、Bluetooth 無線ラジオの他の種類からのトラフィックを検出、ビジー状態のチャネル「ノイズ」としてマークし、周波数がホップ数 には、これらのチャネルを回避できます。 Windows Vista と共有可能な範囲として、「無線」を扱うことで後で AFH さらを向上します。 この機能は、Wi-fi アダプターが使用するチャネルをレポートのワイヤレス テクノロジを使用できます。 Bluetooth スタックがアクティブになったときの通知で報告されたを使用するチャネルし、ノイズの多いとしてマークを付けます。

## <a name="span-idhowdoienableafhinwindowsspanspan-idhowdoienableafhinwindowsspanspan-idhowdoienableafhinwindowsspanhow-do-i-enable-afh-in-windows"></a><span id="How_do_I_enable_AFH_in_Windows_"></span><span id="how_do_i_enable_afh_in_windows_"></span><span id="HOW_DO_I_ENABLE_AFH_IN_WINDOWS_"></span>Windows で AFH を有効にする方法


Windows Vista 以降のバージョン 2.0 と Bluetooth 仕様の以降のバージョンに基づいて Bluetooth 無線 AFH をサポートするために、共有スペクトル モデルが含まれています。 ただし、この機能は既定で無効になります。 共有スペクトルのモデルをサポートするシステムの場合、OEM が明示的に、機能を有効にしての作業中の Wi-fi チャネルをブロックする周波数帯域幅を指定する必要があります。 REG の型の値を作成の周波数帯域幅を指定する\_次のレジストリ キーの下に ChannelAvoidanceRange をという名前の DWORD:

**HKLM\\System\\CurrentControlSet\\Services\\BthServ\\Parameters**

**ChannelAvoidanceRange**値により、またはスペクトルの共有を無効にし、ブロックされている頻度バンドの幅を指定します。 スペクトルの共有を有効にするには設定**ChannelAvoidanceRange**の作業中の Wi-fi チャネルをブロックする周波数帯域幅にします。 単位は MHz であり、範囲は 20 ~ 40 (0.04 を 0.02 GHz)。 Oem は、選択された一連のラジオ アンテナの特性やラジオの製造元からのフィードバックに基づいて適切な帯域幅を決定する必要があります。

新しい**ChannelAvoidanceRange**値では、システムが再起動された後にのみ有効です。 理想的には、OEM が設定する必要があります、 **ChannelAvoidanceRange**プレインストール処理中に値。

効果的に動作する Windows 共有スペクトル モデルでは、Wi-fi ミニポート ドライバーは、ネットワークの接続マネージャーをそのチャネルの使用状況を報告する必要があります。 ネットワーク スタックは、チャネル使用情報を Bluetooth スタックに渡します。

## <a name="span-idhowdoienableremotewakeinwindowsspanspan-idhowdoienableremotewakeinwindowsspanspan-idhowdoienableremotewakeinwindowsspanhow-do-i-enable-remote-wake-in-windows"></a><span id="How_do_I_enable_remote_wake_in_Windows_"></span><span id="how_do_i_enable_remote_wake_in_windows_"></span><span id="HOW_DO_I_ENABLE_REMOTE_WAKE_IN_WINDOWS_"></span>Windows でリモートのスリープ解除を有効にする方法


Windows Vista Service Pack 2 (SP2) 以降のバージョンと Bluetooth 対応キーボードを使用するソフトウェアのサポートを提供して、マウス デバイスがスリープ (S3) からコンピューターをスリープ解除や、システム電源の状態 (S4) を休止状態します。 正常に行う、ウェイクがこのような Bluetooth モジュールが自己供給する必要があり、十分な電力スリープを解除する必要があります。 S4 システム電源の状態からの復帰に Windows により、場合でも、Bluetooth モジュール電源が入っていないコンピューターが S4 になっている場合、コンピューターが復帰しません。

ソフトウェアのリモート スリープ解除を有効にするには、Bluetooth モジュールがウェイク アップをサポートして、次のレジストリ値を設定できますを確認します。

-   HKLM\\システム\\CurrentControlSet\\サービス\\Bthport\\パラメーター \\SystemRemoteWakeSupported:(DWORD) 1
-   HKLM\\システム\\CurrentControlSet\\Enum\\USB\\&lt;vid\_pid&gt;\\&lt;Bluetooth 無線 ID&gt;\\デバイス パラメーター\\RemoteWakeEnabled:(DWORD) 1
-   HKLM\\システム\\CurrentControlSet\\Enum\\USB\\&lt;vid\_pid&gt;\\&lt;Bluetooth 無線 ID&gt;\\デバイス パラメーター\\DeviceRemoteWakeSupported:(DWORD) 1

**注**  デバイス マネージャーで、Bluetooth 無線のプロパティ ページがある場合、**電源管理** タブで、オプションは、ウェイク アップをサポートできます。 ない場合は**電源管理**タブが存在する、ラジオ、ウェイク アップをサポート可能性がありますが、可能性はほとんどありません。

 

 

 





