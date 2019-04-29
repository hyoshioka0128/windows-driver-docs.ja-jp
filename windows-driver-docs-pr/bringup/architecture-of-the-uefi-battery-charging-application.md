---
title: UEFI バッテリが充電アプリケーションのアーキテクチャ
description: Microsoft が提供する UEFI バッテリ充電アプリケーションのアーキテクチャ
ms.assetid: eabac2ec-6e2f-448f-9793-117e12c288d9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e69976ba90a8fd4d87c0d2a29a2e223a05669aa8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328137"
---
# <a name="architecture-of-the-uefi-battery-charging-application-provided-by-microsoft"></a>Microsoft が提供する UEFI バッテリ充電アプリケーションのアーキテクチャ

このトピックでは、UEFI バッテリが充電 Windows 10 Mobile を実行するデバイス用に Microsoft によって提供されるアプリケーションの設計に関する情報を提供します。 Oem はバッテリの充電が、Microsoft のアプリケーションを使用して、または独自のアプリケーションを課金を実装することができます。 Oem 独自 UEFI のバッテリ充電中のアプリケーションを実装する場合がありますの情報を使用このトピックの「ガイドラインとして、設計します。

UEFI バッテリが充電アプリケーションでは、Microsoft が所有しているブート プロセス中に実行される最初のアプリケーションの 1 つです。 UEFI バッテリの充電中のアプリケーションでは、次の主な機能があります。

- デバイスが起動するには、十分な能力を確認します。

- 提供*電源オフ充電*OEM が有効になっている場合をサポートします。 電源オフは、課金の詳細については、次を参照してください。[ブート環境でバッテリが充電中](battery-charging-in-the-boot-environment.md)します。

UEFI バッテリが充電アプリケーションはキーの UEFI プロトコルを使用し、関連のドライバーによって返されるさまざまな状態に反応します。

> [!NOTE]
> 用語*UEFI バッテリの充電アプリケーション*このトピックでは、UEFI のバッテリ充電 mobilestartup.efi によって読み込まれるライブラリを指します。 Mobilestartup.efi の詳細については、次を参照してください。[ブートおよび UEFI](boot-and-uefi.md)します。

## <a name="uefi-protocols-used-by-the-uefi-battery-charging-application"></a>UEFI バッテリが充電アプリケーションによって使用される UEFI プロトコル

UEFI バッテリの充電中アプリケーション (Microsoft が所有) は、以下のセクションで説明されている (Oem によって実装される) プロトコルを使用します。

### <a name="uefi-battery-charging-protocol-efibatterychargingprotocol"></a>UEFI のバッテリ充電プロトコル (EFI\_バッテリ\_充電中\_プロトコル)

次の手順では、UEFI バッテリの充電中のアプリケーションで、UEFI バッテリを充電プロトコルの使用方法の重要な側面について説明します。

1. UEFI バッテリが充電アプリケーションでは、バッテリのハードウェアのリアルタイムの状態をポーリングを使用して[EFI\_バッテリ\_充電中\_プロトコル。GetBatteryInformation](efi-battery-charging-protocolgetbatteryinformation.md) (0x00010002 のバージョンをサポートするデバイスで、 [EFI\_バッテリ\_充電中\_プロトコル](efi-battery-charging-protocol.md)) または[EFI\_バッテリ\_充電中\_プロトコル。GetBatteryStatus](efi-battery-charging-protocolgetbatterystatus.md) (バージョン 0x00010001、EFI をサポートするデバイスで\_バッテリ\_充電中\_プロトコル)。 これらの関数が可能な限りの料金 (SOC) 値の正確な状態を返すことが重要です。 SOC は、OEM が定義したマッピングの状態に基づき (容量、電圧、温度を含む) の値に 0 ~ 100、バッテリの充電量からです。

2. Oem の定義、*メイン OS しきい値ブート*(0 ~ 100 の値)。 この値は、別のデバイス モデルごとに指定できます。 詳細については、*メイン OS しきい値ブート*し、その他のしきい値の値を参照してください[ブート環境でバッテリが充電中](battery-charging-in-the-boot-environment.md)します。

3. バッテリの充電アプリケーションがドライバーから SOC を使用してし、を比較、*メイン OS しきい値ブート*ブートを続行または UEFI で課金するために、ブート プロセスをブロックする必要なかどうかを決定する値。 料金の状態に関するその他の情報を受け取りません。

4. UEFI バッテリのアプリケーションの呼び出しを充電[EFI\_バッテリ\_充電中\_プロトコル。ChargeBattery](efi-battery-charging-protocolchargebattery.md) 、デバイスを充電する待機を**CompletionEvent**対応する[EFI\_バッテリ\_充電中\_の状態](efi-battery-charging-status.md)が返されます。

このプロトコルの詳細については、次を参照してください。 [UEFI バッテリの充電プロトコル](uefi-battery-charging-protocol.md)します。

### <a name="uefi-display-power-state-protocol-efidisplaypowerprotocol"></a>UEFI の電源状態のプロトコルの表示 (EFI\_表示\_POWER\_プロトコル)

UEFI バッテリの充電中のプロセス中に、UEFI のバッテリ充電アプリケーションには、代替の省電力 UI が表示されます。 電源ボタンが押された、アプリケーション呼び出しなし 10 秒後に[EFI\_表示\_POWER\_プロトコル。SetDisplayPowerState](efi-display-power-protocolsetdisplaypowerstate.md)表示とバックライトをオフにします。 これにより、UEFI バッテリの充電中に電力を消費するデバイス、デバイスに対する課金およびメインの OS に迅速に処理できます。 アプリケーションが EFI を呼び出す場合は、ディスプレイがオフに、ユーザーが [電源] ボタンを押す、\_表示\_POWER\_プロトコル。戻り、表示を有効にするには、もう一度 SetDisplayPowerState します。 詳細については、次を参照してください。[ユーザー エクスペリエンス](#user-experience)このトピックで後述します。

このプロトコルの詳細については、次を参照してください。 [UEFI 電源状態のプロトコルを表示する](uefi-display-power-state-protocol.md)します。

### <a name="uefi-usb-function-protocol-efiusbfnioprotocol"></a>UEFI USB 関数プロトコル (EFI\_USBFN\_IO\_プロトコル)

UEFI バッテリが充電アプリケーションが排他的に依拠しています[EFI\_USBFN\_IO\_プロトコル。DetectPort](efi-usbfn-io-protocoldetectport.md)接続されているポートの種類を判断します。 ポートの種類に基づいて、アプリケーションが呼び出す[EFI\_バッテリ\_充電中\_プロトコル。ChargeBattery](efi-battery-charging-protocolchargebattery.md) 1500 mA または 500 のいずれかで mA します。

このプロトコルの詳細については、次を参照してください。 [UEFI USB 関数プロトコル](uefi-usb-function-protocol.md)します。

## <a name="application-logic"></a>アプリケーション ロジック

次の図では、UEFI バッテリが充電アプリケーションの論理手順を説明します。

![uefi のバッテリ充電ロジック](images/oem-battery-charge-logic.png)

次のノートでは、ロジックのいくつか重要なセクションを展開します。

- 呼び出しの前に[EFI\_バッテリ\_充電中\_プロトコル。ChargeBattery](efi-battery-charging-protocolchargebattery.md)、アプリケーション呼び出し[EFI\_USBFN\_IO\_プロトコル。DetectPort](efi-usbfn-io-protocoldetectport.md) USB 充電器を提供できる最大現在を決定します。

  - アプリケーションが専用の壁の充電器または 500 1500 mA を使用するポートが存在する場合は、他のポートの mA します。

  - アプリケーションが 500 を使用するポートが存在するがない場合は、mA します。 この値は無視ワイヤレス充電が必要です。

  - アプリケーションが 500 を使用して存在する充電器がない場合は、mA します。 ただし、アプリケーションが想定[EFI\_バッテリ\_充電中\_プロトコル。ChargeBattery](efi-battery-charging-protocolchargebattery.md)を返す、 [EFI\_バッテリ\_充電中\_完了\_トークン](efi-battery-charging-completion-token.md)の状態で**EfiBatteryChargingSourceNotDetected**します。

- 場合は、OEM する必要があります、デバイスと維持充電器安全な運用リージョン内で。

- デバイスのバッテリはありませんが、アプリケーションが接続されている電源に接続がある場合[EFI\_バッテリ\_充電中\_プロトコル。ChargeBattery](efi-battery-charging-protocolchargebattery.md)バッテリを充電する UEFI バッテリのドライバーを充電が返す必要があります**EfiBatteryChargingStatusBatteryNotDetected**します。 アプリケーションでは、UI エラーを表示して、デバイスをシャット ダウンしてこのエラーを処理します。

- [EFI\_バッテリ\_充電中\_状態](efi-battery-charging-status.md)の値は、両方で同じ方法で解釈されます*しきい値充電*と*充電電源オフ*以外のモード**EfiBatteryChargingStatusSuccess**します。 これらのモードを課金の詳細については、次を参照してください。[ブート環境でバッテリが充電中](battery-charging-in-the-boot-environment.md)します。

- 課金モードで、デバイスがある場合、電源を切断するが結果として予想ファームウェアを使用してアプリケーションをシグナル通知の**EfiBatteryChargingSourceNotDetected**、その結果、アプリケーションのシャット ダウンしていますデバイスです。

- ファームウェアが、アプリケーションの状態を通知するかどうか**EfiBatteryChargingStatusOverheat**または**EfiBatteryChargingStatusTimeout**、5 分 (ただし、アプリケーションの充電中、デバイスの一時停止まだ呼び出し[EFI\_バッテリ\_充電中\_プロトコル。GetBatteryInformation](efi-battery-charging-protocolgetbatteryinformation.md)または[EFI\_バッテリ\_充電中\_プロトコル。GetBatteryStatus](efi-battery-charging-protocolgetbatterystatus.md)約 1 秒間隔で)。 5 分後、デバイスが再開される呼び出して充電[EFI\_バッテリ\_充電中\_プロトコル。ChargeBattery](efi-battery-charging-protocolchargebattery.md)します。 これらの 5 分では、中にファームウェアが予想されますと適切なアプリケーションによって提供されるイベントを通知する[EFI\_バッテリ\_充電中\_状態](efi-battery-charging-status.md)値 (たとえば、ソース切断を通知する必要があります**EfiBatteryChargingSourceNotDetected**)。

- どちらの課金モードというラベルの付いたボックス中に関連するアニメーション化された UI が表示されます**アプリで維持**前の図。

- *電源オフ充電*モード、イベントがシグナル状態、ファームウェアの状態の場合**EfiBatteryChargingStatusSuccess**、UEFI バッテリが充電までメインの OS にアプリケーションが起動しません。ユーザーは、3 秒の電源ボタンを保持します。 ただし、アプリケーションでは、この時点で、USB ケーブルが切断されたことを検出するデバイスを電源オフは、します。 UEFI バッテリが充電アプリケーションでは、ドライバーが完全にバッテリを維持する必要があります*電源オフ モードを充電*します。

- *電源オフ モードを充電*ファームウェアがシグナル状態、エラーまたは成功イベントでない限り、アプリケーションを課金 UEFI バッテリの電源が入らないデバイス オフします。

### <a name="error-handling"></a>エラー処理

毎回[EFI\_バッテリ\_充電中\_プロトコル。ChargeBattery](efi-battery-charging-protocolchargebattery.md)が呼び出される、 [EFI\_バッテリ\_充電中\_完了\_トークン](efi-battery-charging-completion-token.md)を指定します。 トークン内のイベントがシグナル状態ドライバーにエラーが発生した場合、 [EFI\_バッテリ\_充電中\_状態](efi-battery-charging-status.md)します。 次の表は、UEFI バッテリが充電アプリケーションがさまざまな状況でさまざまな状態の値に反応する方法を示しています。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>状態</th>
<th>しきい値の充電中モード</th>
<th>電源オフ (前後の充電状態がしきい値に達した) モードの課金</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EfiBatteryChargingStatusNoneNone</p></td>
<td><p>いない予想/無効</p></td>
<td><p>いない予想/無効</p></td>
</tr>
<tr class="even">
<td><p>EfiBatteryChargingStatusSuccess</p></td>
<td><p>オペレーティング システムをブート</p></td>
<td><p><strong>前に、料金の状態では、しきい値に達した。</strong>電源オフ課金モードで続行します。</p>
<p><strong>料金の状態では、しきい値に達すると。</strong>USB が切断されるまでに、課金モード電源オフのまま</p></td>
</tr>
<tr class="odd">
<td><p>EfiBatteryChargingStatusOverheat</p></td>
<td><p>5 分の課金を一時停止し、し、課金を再開</p></td>
<td><p>5 分の課金を一時停止し、し、課金を再開</p></td>
</tr>
<tr class="even">
<td><p>EfiBatteryChargingStatusVoltageOutOfRange</p></td>
<td><p>オペレーティング システムをブート</p></td>
<td><p>オペレーティング システムをブート</p></td>
</tr>
<tr class="odd">
<td><p>EfiBatteryChargingStatusCurrentOutOfRange</p></td>
<td><p>オペレーティング システムをブート</p></td>
<td><p>オペレーティング システムをブート</p></td>
</tr>
<tr class="even">
<td><p>EfiBatteryChargingStatusTimeout</p></td>
<td><p>5 分の課金を一時停止し、し、課金を再開</p></td>
<td><p>5 分の課金を一時停止し、し、課金を再開</p></td>
</tr>
<tr class="odd">
<td><p>EfiBatteryChargingStatusAborted</p></td>
<td><p>10 秒間エラー UI を表示しをシャット ダウン</p></td>
<td><p>10 秒間エラー UI を表示しをシャット ダウン</p></td>
</tr>
<tr class="even">
<td><p>EfiBatteryChargingStatusDeviceError</p></td>
<td><p>10 秒間エラー UI を表示しをシャット ダウン</p></td>
<td><p>10 秒間エラー UI を表示しをシャット ダウン</p></td>
</tr>
<tr class="odd">
<td><p>EfiBatteryChargingStatusExtremeCold</p></td>
<td><p>10 秒間エラー UI を表示しをシャット ダウン</p></td>
<td><p>10 秒間エラー UI を表示しをシャット ダウン</p></td>
</tr>
<tr class="even">
<td><p>EfiBatteryChargingStatusBatteryChargingNotSupported</p></td>
<td><p>10 秒間エラー UI を表示しをシャット ダウン</p></td>
<td><p>10 秒間エラー UI を表示しをシャット ダウン</p></td>
</tr>
<tr class="odd">
<td><p>EfiBatteryChargingStatusBatteryNotDetected</p></td>
<td><p>10 秒間エラー UI を表示しをシャット ダウン</p></td>
<td><p>10 秒間エラー UI を表示しをシャット ダウン</p></td>
</tr>
<tr class="even">
<td><p>EfiBatteryChargingSourceNotDetected</p></td>
<td><p>シャットダウン</p></td>
<td><p>シャットダウン</p></td>
</tr>
<tr class="odd">
<td><p>EfiBatteryChargingSourceVoltageInvalid</p></td>
<td><p>10 秒間エラー UI を表示しをシャット ダウン</p></td>
<td><p>10 秒間エラー UI を表示しをシャット ダウン</p></td>
</tr>
<tr class="even">
<td><p>EfiBatteryChargingSourceCurrentInvalid</p></td>
<td><p>10 秒間エラー UI を表示しをシャット ダウン</p></td>
<td><p>10 秒間エラー UI を表示しをシャット ダウン</p></td>
</tr>
<tr class="odd">
<td><p>EfiBatteryChargingErrorRequestShutdown</p></td>
<td><p>シャットダウン</p></td>
<td><p>シャットダウン</p></td>
</tr>
<tr class="even">
<td><p>EfiBatteryChargingErrorRequestReboot</p></td>
<td><p>再起動します</p></td>
<td><p>再起動します</p></td>
</tr>
</tbody>
</table>

次の表は、UEFI のバッテリ充電アプリケーションの反応から受信した状態の値を[EFI\_バッテリ\_充電中\_プロトコル。GetBatteryInformation](efi-battery-charging-protocolgetbatteryinformation.md)または[EFI\_バッテリ\_充電中\_プロトコル。GetBatteryStatus](efi-battery-charging-protocolgetbatterystatus.md)します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>状態</th>
<th>しきい値の充電中モード</th>
<th>電源オフ (前後の充電状態がしきい値に達した) モードの課金</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EFI_SUCCESS</p>
<p>エラーが検出されなかった場合は、この値が返されます。</p></td>
<td><p>適用なし</p></td>
<td><p>適用なし</p></td>
</tr>
<tr class="even">
<td><p>EFI_INVALID_PARAMETER</p>
<p>入力パラメーターが正しくない場合は、この値が返されます。 これは、理論的にすることはできません、実稼働環境で使用できます。</p></td>
<td><p>10 秒間エラー UI を表示しをシャット ダウン</p></td>
<td><p>10 秒間エラー UI を表示しをシャット ダウン</p></td>
</tr>
<tr class="odd">
<td><p>EFI_DEVICE_ERROR または EFI_NOT_READY</p>
<p>これらのエラー条件は、同じ方法で処理されます。 これらの値によって返される<a href="efi-battery-charging-protocolgetbatteryinformation.md" data-raw-source="[EFI_BATTERY_CHARGING_PROTOCOL.GetBatteryInformation](efi-battery-charging-protocolgetbatteryinformation.md)">EFI_BATTERY_CHARGING_PROTOCOL します。GetBatteryInformation</a>または<a href="efi-battery-charging-protocolgetbatterystatus.md" data-raw-source="[EFI_BATTERY_CHARGING_PROTOCOL.GetBatteryStatus](efi-battery-charging-protocolgetbatterystatus.md)">EFI_BATTERY_CHARGING_PROTOCOL します。GetBatteryStatus</a>デバイスがいくつかのデバイスのエラーのための主なオペレーティング システムを起動していない可能性がある場合。 特に、次の点で異なります。</p>
<ul>
<li><p>EfiBatteryChargingStatusAborted</p></li>
<li><p>EfiBatteryChargingStatusDeviceError</p></li>
<li><p>EfiBatteryChargingStatusExtremeCold</p></li>
<li><p>EfiBatteryChargingStatusBatteryChargingNotSupported</p></li>
<li><p>EfiBatteryChargingStatusBatteryNotDetected</p></li>
<li><p>EfiBatteryChargingSourceVoltageInvalid</p></li>
<li><p>EfiBatteryChargingSourceCurrentInvalid</p></li>
<li><p>EfiBatteryChargingErrorRequestShutdown</p></li>
<li><p>EfiBatteryChargingErrorRequestReboot</p></li>
</ul>
<p>EFI_DEVICE_ERROR または後ろに上記のエラーのいずれかの入力候補トークン EFI_NOT_READY をスローすると、最終的にシャット ダウンするデバイスが発生します。</p></td>
<td><p>再開し、呼び出す<a href="efi-battery-charging-protocolchargebattery.md" data-raw-source="[EFI_BATTERY_CHARGING_PROTOCOL.ChargeBattery](efi-battery-charging-protocolchargebattery.md)">EFI_BATTERY_CHARGING_PROTOCOL します。ChargeBattery</a></p></td>
<td><p>再開し、呼び出す<a href="efi-battery-charging-protocolchargebattery.md" data-raw-source="[EFI_BATTERY_CHARGING_PROTOCOL.ChargeBattery](efi-battery-charging-protocolchargebattery.md)">EFI_BATTERY_CHARGING_PROTOCOL します。ChargeBattery</a></p></td>
</tr>
</tbody>
</table>

## <a name="user-experience"></a>ユーザー エクスペリエンス

次の図は、バッテリに十分な料金がない場合、UEFI バッテリが充電アプリケーションで、UI 画面に描画する方法、またはかどうかに、デバイスが*電源オフ モードを充電*します。

![バッテリの充電中のユーザー エクスペリエンス](images/oem-battery-charge-user-experience.png)

次の手順では、アプリケーションが画面に UI を描画する方法について説明します。

- アプリケーションでは、フレーム内のすべてのピクセルに背景の塗りつぶしの色を記述することで、画面をクリアします。

- アプリケーションでは、画面に直接ビットマップ バッファーからピクセルをコピーして交互バッテリ UI ビットマップを描画します。 電源ボタンが押された、アプリケーション呼び出しせずに 10 秒を渡す場合[EFI\_表示\_POWER\_プロトコル。SetDisplayPowerState](efi-display-power-protocolsetdisplaypowerstate.md)表示とバックライトをオフにします。 ユーザーは、EFI、電源ボタンを押した場合\_表示\_POWER\_プロトコル。SetDisplayPowerState はディスプレイをオンにすると呼ばれます。

- ドライバーからアプリケーションがエラーを受け取ると、アプリケーション、フレーム バッファー内のすべてのピクセルに背景の塗りつぶしの色を記述することで、画面をクリアして、アプリケーションが適切なビットマップからピクセルをコピーしてバッテリ エラー画面に描画し、直接表示するバッファー。
