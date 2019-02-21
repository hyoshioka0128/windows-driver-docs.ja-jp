---
title: WDDM 1.2 以降のシームレスな状態遷移を提供します。
description: いくつかの機能は、ブート プロセス、電力の少ない状態から遷移、およびオペレーティング システムのコントロールに遷移中に画面の点滅を最小限に抑えるのに役立ちます。
ms.assetid: CD2208AA-62B6-4BAD-BE7C-0791B13D1E96
keywords:
- 状態遷移の WDK の表示
- WDK の表示を休止状態から再開します。
- ファームウェア モード ドライバー WDK の表示を表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 110fad8e532db83f0010651275cc867add39de5f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558336"
---
# <a name="providing-seamless-state-transitions-in-wddm-12-and-later"></a>WDDM 1.2 以降のシームレスな状態遷移を提供します。


以降 Windows 8 では、いくつかの機能を画面の点滅を排除または最小限に役立つ、ちらつきのブート プロセス中に、電力の少ない状態から遷移中に、および遷移中にでは、チェックをドライバーをアップグレードまたはシステムのバグのオペレーティング システムのコントロールに戻します。 さらに、Windows 8 およびそれ以降のコンピューターでシステム ファームウェアでは、時の電源をパネルを表示し、オペレーティング システムにこの情報を渡すネイティブの解像度との統合されたタイミングを検出する必要があります。 Windows 表示 Driver Model (WDDM) 1.2 および以降の表示のミニポート ドライバーには、この動作をサポートする必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">WDDM の最小バージョン</td>
<td align="left">1.2</td>
</tr>
<tr class="even">
<td align="left">Windows の最小バージョン</td>
<td align="left">8</td>
</tr>
<tr class="odd">
<td align="left">ドライバーの実装: 完全なグラフィックスおよび表示のみ</td>
<td align="left">必須</td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit" data-raw-source="[WHCK](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)">WHCK</a>要件とテスト</td>
<td align="left"><p><strong>System.Client.Firmware.UEFI.GOP.Display</strong></p>
<p><strong>Device.Graphics.PnpStopStartSupport</strong></p>
<p><strong>Device.Graphics…DisplayOutputControl</strong></p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idtransitionfromfirmwaretooperatingsystemspanspan-idtransitionfromfirmwaretooperatingsystemspanspan-idtransitionfromfirmwaretooperatingsystemspantransition-from-firmware-to-operating-system"></a><span id="Transition_from_firmware_to_operating_system"></span><span id="transition_from_firmware_to_operating_system"></span><span id="TRANSITION_FROM_FIRMWARE_TO_OPERATING_SYSTEM"></span>ファームウェアからオペレーティング システムへの移行します。


クライアントの Sku の対象となるすべての Windows 8 システムでは、Unified Extensible Firmware Interface (UEFI) グラフィックス出力プロトコル (GOP) をサポートする必要があります。 起動フェーズでは、GOP は、システムの統合表示パネルのネイティブのタイミングとネイティブの解像度を設定します。 オペレーティング システムのディスプレイの所有権を取得する準備ができたら、GOP は、表示するためにスキャンを使用できる、フレーム バッファーを渡します。 この時点では、オペレーティング システムは、タイミングを表示または解像度をリセットしようとしないが、単にされるため、1 つの画面の点滅、指定したフレーム バッファーを使用します。

**ハードウェア認定要件**

この機能を実装するときにハードウェア デバイスが満たす必要のある要件については、関連するを参照してください[WHCK ドキュメント](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)で**System.Client.Firmware.UEFI.GOP.Display**します。

## <a name="span-idtransitionfromoperatingsystemtodriverspanspan-idtransitionfromoperatingsystemtodriverspanspan-idtransitionfromoperatingsystemtodriverspantransition-from-operating-system-to-driver"></a><span id="Transition_from_operating_system_to_driver"></span><span id="transition_from_operating_system_to_driver"></span><span id="TRANSITION_FROM_OPERATING_SYSTEM_TO_DRIVER"></span>オペレーティング システムからドライバーへの移行します。


呼び出すことによって、デバイスのプラグ アンド プレイ (PnP) 開始が開始しますオペレーティング システムは、WDDM ドライバーを起動した後、表示の所有権を渡す時に、 [ *DxgkDdiStartDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff560775)関数。 または、休止状態から再開した後、オペレーティング システムの起動時、デバイスを呼び出して、 [ *DxgkDdiSetPowerState* ](https://msdn.microsoft.com/library/windows/hardware/ff560764)関数と、 *DeviceUid*パラメーター設定**表示\_アダプター\_HW\_ID** (Video.h で定義されている)。 この時点で通常画面空白になり (黒として表示されます)、WDDM グラフィックス ドライバー コントロールの実行中にします。

ドライバーを呼び出すことができます、 [ **DxgkCbAcquirePostDisplayOwnership** ](https://msdn.microsoft.com/library/windows/hardware/hh451339)クエリと表示の現在のフレーム バッファーの正確な状態用のオペレーティング システム (Windows 8 で利用可能なから開始) 関数ファームウェアとブート ローダーによって設定されているモードです。 情報を[ **DXGK\_表示\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh464017)構造は、この関数によって取得されたドライバー表示コント ローラーを維持する可能性がありますし、モニターの再同期をされません。 ドライバーもの詳細については、フレーム バッファー、ためにより滑らかな遷移を実行することができます。

PnP 開始の詳細についてで指定[プラグ アンド プレイ (PnP) および WDDM 1.2 以降](plug-and-play--pnp--start-and-stop-cases.md)します。

## <a name="span-idtransitionfromdrivertooperatingsystemspanspan-idtransitionfromdrivertooperatingsystemspanspan-idtransitionfromdrivertooperatingsystemspantransition-from-driver-to-operating-system"></a><span id="Transition_from_driver_to_operating_system"></span><span id="transition_from_driver_to_operating_system"></span><span id="TRANSITION_FROM_DRIVER_TO_OPERATING_SYSTEM"></span>ドライバーからオペレーティング システムへの移行します。


オペレーティング システムは呼び出すことによって、ディスプレイ デバイスの PnP 停止を要求することができます、 [ *DxgkDdiStopDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff560781)関数。 この時点で通常画面は空白になり (黒として表示されます)、オペレーティング システムの表示コントロール上で実行中にします。 オペレーティング システムを呼び出すことができます、 [ *DxgkDdiStopDeviceAndReleasePostDisplayOwnership* ](https://msdn.microsoft.com/library/windows/hardware/hh451415)用に構成されたフレーム バッファーを設定する WDDM ドライバーを必要とする (Windows 8 で利用可能なから開始) 関数スキャンします。オペレーティング システムは、スムーズな移行を実行できるように、ディスプレイのコントロールでは、このフレーム バッファーにレンダリングできます。

詳細については、追加のシナリオを含む、PnP の停止がで指定された[プラグ アンド プレイ (PnP) および WDDM 1.2 以降](plug-and-play--pnp--start-and-stop-cases.md)します。

**ハードウェア認定要件**

このハンドオフの詳細については、関連するを参照してください[WHCK ドキュメント](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)で**Device.Graphics.PnpStopStartSupport**します。

## <a name="span-idtransitiontooperatingsystemwithoutdisablingdriverspanspan-idtransitiontooperatingsystemwithoutdisablingdriverspanspan-idtransitiontooperatingsystemwithoutdisablingdriverspantransition-to-operating-system-without-disabling-driver"></a><span id="Transition_to_operating_system_without_disabling_driver"></span><span id="transition_to_operating_system_without_disabling_driver"></span><span id="TRANSITION_TO_OPERATING_SYSTEM_WITHOUT_DISABLING_DRIVER"></span>ドライバーを無効にせずにオペレーティング システムを移行します。


場合がありますオペレーティング システムでは、回復不可能なエラーが発生し、システムのバグ チェックを発行する必要があります。 この場合、オペレーティング システムが、表示を制御する必要がありますが、WDDM ドライバーを停止する機能がない場合があります。 WDDM 1.2 およびそれ以降のドライバーが実装するために必要な[ *DxgkDdiSystemDisplayEnable* ](https://msdn.microsoft.com/library/windows/hardware/hh451426)と[ *DxgkDdiSystemDisplayWrite* ](https://msdn.microsoft.com/library/windows/hardware/hh451429)関数は、オペレーティング システムをシームレスにできるは、高解像度や色深度にグラフィカル インターフェイスを維持しながら、エラー画面を表示できる状態に移行します。 この移行では、少し目障りな感じユーザー エクスペリエンスを排除します。

**ハードウェア認定要件**

この機能を実装するときにハードウェア デバイスが満たす必要のある要件については、関連するを参照してください[WHCK ドキュメント](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)で**Device.Graphics.DisplayOutputControl**します。

## <a name="span-idwindows8firmwaremodechangesspanspan-idwindows8firmwaremodechangesspanspan-idwindows8firmwaremodechangesspanwindows8-firmware-mode-changes"></a><span id="Windows_8_firmware_mode_changes"></span><span id="windows_8_firmware_mode_changes"></span><span id="WINDOWS_8_FIRMWARE_MODE_CHANGES"></span>Windows 8 ファームウェア モードの変更


これらは、オペレーティング システムに制御をファームウェア手の前に、ファームウェアの表示モードに変更します。

<span id="_1.2_and_later_drivers__dxgkddi_interface_version____dxgkddi_interface_version_win8_"></span><span id="_1.2_AND_LATER_DRIVERS__DXGKDDI_INTERFACE_VERSION____DXGKDDI_INTERFACE_VERSION_WIN8_"></span>WDDM 1.2 およびそれ以降のドライバー (**DXGKDDI\_インターフェイス\_バージョン** &gt; =  **DXGKDDI\_インターフェイス\_バージョン\_WIN8**)  
さらに Windows 8 では、以降では、表示が点滅を排除するために Int10 モード変更要求は呼び出されませんファームウェアおよび WDDM 1.2 およびそれ以降のドライバー。

さらに、モニターがになっている間にモードの変更が発生した場合、オペレーティング システムを呼び出す、 [ *DxgkDdiCommitVidPn* ](https://msdn.microsoft.com/library/windows/hardware/ff559597)関数の 1 回だけで、 *pCommitVidPnArg*モニターがオンの場合は、値に設定するパラメーター、および**PathPoweredOff**のメンバー *pCommitVidPnArg* - &gt; **フラグ**設定**TRUE**します。

<span id="_1.0_and_1.1_drivers__DXGKDDI_INTERFACE_VERSION___DXGKDDI_INTERFACE_VERSION_WIN8_"></span><span id="_1.0_and_1.1_drivers__dxgkddi_interface_version___dxgkddi_interface_version_win8_"></span><span id="_1.0_AND_1.1_DRIVERS__DXGKDDI_INTERFACE_VERSION___DXGKDDI_INTERFACE_VERSION_WIN8_"></span>WDDM 1.0 と 1.1 ドライバー (**DXGKDDI\_インターフェイス\_バージョン** &lt; **DXGKDDI\_インターフェイス\_バージョン\_WIN8**)  
WDDM version 1.0 および 1.1 のドライバーをブート プロセス中に、または休止状態から再開するときに、Windows 8 で実行されている Int10 VGA モード 0x12 への呼び出しになるは、モニターのネイティブの高解像度にディスプレイの解像度を設定します。 Windows 8 では、前に、Int10 VGA モード 0x12 呼び出しに 640 x 480 ピクセル、ピクセルあたり 16 ビットのオペレーティング システムのスプラッシュ スクリーン イメージを表示する、点滅カーソルなしでディスプレイの解像度を設定します。

一方、WDDM のバージョンの VGA モード 0x12 のブートで Windows 8 以降、高解像度モードをサポートしていないかを示す 1.0 および 1.1 のドライバー設定ディスプレイの解像度に 640 x 480 ピクセルで 16 ビット/ピクセル、点滅カーソルなしで。 システムの休止状態から再開時に、モニターのネイティブの高解像度にもディスプレイの解像度が設定されます。

さらに、モニターがになっている間にモードの変更が発生した場合、オペレーティング システムを呼び出す、 [ *DxgkDdiCommitVidPn* ](https://msdn.microsoft.com/library/windows/hardware/ff559597) WDDM 1.2 ドライバーでは、上記で説明したとおりに機能し、呼び出す*DxgkDdiCommitVidPn* 、 *2 番目*を空にビデオ存在するネットワーク (VidPN) までの時間*pCommitVidPnArg* - &gt; **hFunctionalVidPn** 、および none に設定した値のフラグの*pCommitVidPnArg*-&gt;**フラグ**します。

この 2 つの部分の呼び出しシーケンスは、システムが休止状態の後に再開し、モニターの同期の生成は、有効にしておくにも発生します。 ここで、ドライバーが操作は不要 2 番目の呼び出しを受信すると[ *DxgkDdiCommitVidPn*](https://msdn.microsoft.com/library/windows/hardware/ff559597)します。

 

 





