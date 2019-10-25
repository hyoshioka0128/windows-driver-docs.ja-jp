---
title: WDDM 1.2 以降でのシームレスな状態遷移の提供
description: いくつかの機能を使用して、ブートプロセス中の画面の点滅を最小限に抑え、低い電源状態から移行して、オペレーティングシステムの制御に戻すことができます。
ms.assetid: CD2208AA-62B6-4BAD-BE7C-0791B13D1E96
keywords:
- 状態遷移 WDK 表示
- 休止状態の WDK ディスプレイから再開する
- ディスプレイドライバーでのファームウェアモード WDK 表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42500440bec5adee9c608139d34e31d974df13a4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829511"
---
# <a name="providing-seamless-state-transitions-in-wddm-12-and-later"></a>WDDM 1.2 以降でのシームレスな状態遷移の提供


Windows 8 以降、いくつかの機能を使用して、ブートプロセス中、低い電源状態からの移行中、ドライバーのアップグレード時やシステムのバグチェック時のオペレーティングシステム制御への移行中に、画面の点滅を最小化または除去することができます。 さらに、Windows 8 以降のコンピューターのシステムファームウェアは、電源をオンにしてこの情報をオペレーティングシステムに渡すときに、統合された表示パネルのネイティブの解像度とタイミングを検出する必要があります。 Windows Display Driver Model (WDDM) 1.2 以降では、この動作がサポートされている必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">最小 WDDM バージョン</td>
<td align="left">1.2</td>
</tr>
<tr class="even">
<td align="left">Windows の最小バージョン</td>
<td align="left">8</td>
</tr>
<tr class="odd">
<td align="left">ドライバーの実装—完全なグラフィックスと表示のみ</td>
<td align="left">Mandatory</td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit" data-raw-source="[WHCK](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)">必要条件</a>とテスト</td>
<td align="left"><p><strong>システム......。</strong></p>
<p><strong>デバイス...PnpStopStartSupport</strong></p>
<p><strong>デバイス...DisplayOutputControl</strong></p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idtransition_from_firmware_to_operating_systemspanspan-idtransition_from_firmware_to_operating_systemspanspan-idtransition_from_firmware_to_operating_systemspantransition-from-firmware-to-operating-system"></a><span id="Transition_from_firmware_to_operating_system"></span><span id="transition_from_firmware_to_operating_system"></span><span id="TRANSITION_FROM_FIRMWARE_TO_OPERATING_SYSTEM"></span>ファームウェアからオペレーティングシステムへの移行


クライアント Sku を対象とするすべての Windows 8 システムは、Unified Extensible Firmware Interface (UEFI) グラフィックス出力プロトコル (GOP) をサポートしている必要があります。 起動フェーズでは、GOP はシステムの統合された表示パネルにネイティブのタイミングとネイティブの解像度を設定します。 オペレーティングシステムがディスプレイの所有権を引き継ぐ準備ができたら、GOP はディスプレイをスキャンするために使用できるフレームバッファーをハンドオフします。 現時点では、オペレーティングシステムはディスプレイのタイミングや解像度をリセットしようとしませんが、単に指定されたフレームバッファーを使用するので、1つの画面フラッシュが不要になります。

**ハードウェア認定の要件**

ハードウェアデバイスがこの機能を実装するときに満たす必要がある要件の詳細については、「 [」を参照](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)**してください。**

## <a name="span-idtransition_from_operating_system_to_driverspanspan-idtransition_from_operating_system_to_driverspanspan-idtransition_from_operating_system_to_driverspantransition-from-operating-system-to-driver"></a><span id="Transition_from_operating_system_to_driver"></span><span id="transition_from_operating_system_to_driver"></span><span id="TRANSITION_FROM_OPERATING_SYSTEM_TO_DRIVER"></span>オペレーティングシステムからドライバーへの移行


ブート後にオペレーティングシステムによってディスプレイの所有権が WDDM ドライバーに渡されると、 [*DxgkDdiStartDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_start_device)関数を呼び出すことによってデバイスのプラグアンドプレイ (PnP) 開始が開始されます。 また、休止状態から再開した後、オペレーティングシステムは、 [*DxgkDdiSetPowerState*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_set_power_state)関数を呼び出して、デバイスを起動します。これには、 *DeviceUid*パラメーターを設定して、 **\_アダプター\_HW\_ID** (で定義) を表示します。ビデオ. h)。 この時点で、WDDM グラフィックスドライバーはコントロールを取得しますが、通常は画面が非表示になり (黒でレンダリングされます)、

ドライバーは、 [**DxgkCbAcquirePostDisplayOwnership**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_acquire_post_display_ownership)関数 (Windows 8 以降で使用可能) を呼び出して、現在のフレームバッファーと、ファームウェアとブートローダーによって設定された表示モードの正確な状態をオペレーティングシステムに照会できます。 この関数によって取得された情報構造[ **\_DXGK\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgk_display_information)に情報が表示されているので、ドライバーはディスプレイコントローラーをアクティブにしたままにして、モニターの再同期を行わないようにすることができます。 ドライバーにはフレームバッファーに関する詳細情報も含まれているため、より滑らかな遷移を実行できます。

PnP 開始の詳細については[、WDDM 1.2 以降のプラグアンドプレイ (pnp)](plug-and-play--pnp--start-and-stop-cases.md)に記載されています。

## <a name="span-idtransition_from_driver_to_operating_systemspanspan-idtransition_from_driver_to_operating_systemspanspan-idtransition_from_driver_to_operating_systemspantransition-from-driver-to-operating-system"></a><span id="Transition_from_driver_to_operating_system"></span><span id="transition_from_driver_to_operating_system"></span><span id="TRANSITION_FROM_DRIVER_TO_OPERATING_SYSTEM"></span>ドライバーからオペレーティングシステムへの移行


オペレーティングシステムは、 [*DxgkDdiStopDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_stop_device)関数を呼び出すことによって、ディスプレイデバイスの PnP 停止を要求できます。 この時点では、オペレーティングシステムがディスプレイコントロールを引き継ぐ間に、画面が非表示になり (黒でレンダリング) されます。 オペレーティングシステムは、WDDM ドライバーがスキャン用に構成されたフレームバッファーを設定する必要がある[*DxgkDdiStopDeviceAndReleasePostDisplayOwnership*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_stop_device_and_release_post_display_ownership)関数 (Windows 8 以降で利用可能) を呼び出すことができます。オペレーティングシステムはディスプレイの制御中にこのフレームバッファーにレンダリングできるため、スムーズな移行を実行できます。

追加のシナリオを含む、PnP 停止の詳細については、 [WDDM 1.2 以降のプラグアンドプレイ (pnp)](plug-and-play--pnp--start-and-stop-cases.md)を参照してください。

**ハードウェア認定の要件**

このハンドオフの詳細については、デバイスの関連する[whck ドキュメント](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)を参照してください. **.PnpStopStartSupport**。

## <a name="span-idtransition_to_operating_system_without_disabling_driverspanspan-idtransition_to_operating_system_without_disabling_driverspanspan-idtransition_to_operating_system_without_disabling_driverspantransition-to-operating-system-without-disabling-driver"></a><span id="Transition_to_operating_system_without_disabling_driver"></span><span id="transition_to_operating_system_without_disabling_driver"></span><span id="TRANSITION_TO_OPERATING_SYSTEM_WITHOUT_DISABLING_DRIVER"></span>ドライバーを無効にせずにオペレーティングシステムに移行する


オペレーティングシステムで回復不能なエラーが発生し、システムのバグチェックを発行する必要がある場合があります。 この問題が発生した場合、オペレーティングシステムがディスプレイを制御する必要がありますが、WDDM ドライバーを停止することはできません。 [*DxgkDdiSystemDisplayEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_system_display_enable)および[*DxgkDdiSystemDisplayWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_system_display_write)関数を実装するには、WDDM 1.2 以降のドライバーが必要です。これにより、オペレーティングシステムは、エラー画面を表示できる状態にシームレスに移行できます。高い解像度と色数でグラフィカルインターフェイスを維持します。 この移行により、目障りのユーザーエクスペリエンスが排除します。

**ハードウェア認定の要件**

ハードウェアデバイスがこの機能を実装するときに満たす必要がある要件の詳細[について](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)は、**デバイス...DisplayOutputControl**。

## <a name="span-idwindows_8_firmware_mode_changesspanspan-idwindows_8_firmware_mode_changesspanspan-idwindows_8_firmware_mode_changesspanwindows8-firmware-mode-changes"></a><span id="Windows_8_firmware_mode_changes"></span><span id="windows_8_firmware_mode_changes"></span><span id="WINDOWS_8_FIRMWARE_MODE_CHANGES"></span>Windows 8 ファームウェアモードの変更


ファームウェアがオペレーティングシステムを制御する前に、ファームウェアの表示モードが変更されています。

<span id="_1.2_and_later_drivers__dxgkddi_interface_version____dxgkddi_interface_version_win8_"></span><span id="_1.2_AND_LATER_DRIVERS__DXGKDDI_INTERFACE_VERSION____DXGKDDI_INTERFACE_VERSION_WIN8_"></span>WDDM 1.2 以降のドライバー (**dxgkddi\_interface\_version** &gt;= **DXGKDDI\_interface\_VERSION\_WIN8**)  
Windows 8 以降では、ディスプレイの点滅をさらに解消するために、Int10 モードの変更要求は、WDDM 1.2 以降のドライバーのファームウェアでは呼び出されません。

また、モニターがオフになっている間にモードが変更された場合、オペレーティングシステムは[*DxgkDdiCommitVidPn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_commitvidpn)関数を1回だけ呼び出します。このとき、 *pCommitVidPnArg*パラメーターには、モニターが有効になっている場合と同じ値に設定され、**PathPoweredOff**の*pCommitVidPnArg*のメンバー-&gt;**フラグ**が**TRUE**に設定されています。

<span id="_1.0_and_1.1_drivers__DXGKDDI_INTERFACE_VERSION___DXGKDDI_INTERFACE_VERSION_WIN8_"></span><span id="_1.0_and_1.1_drivers__dxgkddi_interface_version___dxgkddi_interface_version_win8_"></span><span id="_1.0_AND_1.1_DRIVERS__DXGKDDI_INTERFACE_VERSION___DXGKDDI_INTERFACE_VERSION_WIN8_"></span>WDDM 1.0 および1.1 ドライバー (**dxgkddi\_interface\_version** &lt; **dxgkddi\_interface\_version\_WIN8**)  
Windows 8 で実行されている WDDM バージョン1.0 および1.1 ドライバーの場合、ブートプロセス中、または休止状態からの再開時に、モニターのネイティブ高解像度にディスプレイの解像度を設定する Int10 VGA モード0x12 への呼び出しが行われます。 Windows 8 より前の Int10 VGA モードの0x12 呼び出しでは、ディスプレイの解像度が 640 x 480 ピクセルに設定されており、点滅するカーソルがない状態で、オペレーティングシステムのスプラッシュスクリーンイメージが表示されます。

ただし、WDDM バージョン1.0 および1.1 ドライバーが高解像度モードをサポートしていないことを示している場合、Windows 8 以降では、0x12 が VGA モードでブートされ、ディスプレイの解像度が 640 x 480 ピクセルに設定されます (ピクセルあたり16ビット)。点滅するカーソルはありません。 システムが休止状態から再開した場合、ディスプレイの解像度はモニターのネイティブ高解像度に設定されたままになります。

また、モニターがオフになっている間にモードの変更が発生した場合、オペレーティングシステムは、前述の WDDM 1.2 ドライバーの[*DxgkDdiCommitVidPn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_commitvidpn)関数を呼び出し、 *DxgkDdiCommitVidPn*を空にして*もう*一度呼び出します。*pCommitVidPnArg*-&gt;**hFunctionalVidPn**の Video present ネットワーク (VidPN)、および*pCommitVidPnArg*-&gt;**フラグ**で設定されているフラグ値はありません。

この2部構成の呼び出しシーケンスは、システムが休止状態の後に再開され、モニターの同期生成が有効なままになる場合にも発生します。 この場合、 [*DxgkDdiCommitVidPn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_commitvidpn)への2回目の呼び出しを受信しても、ドライバーは何も実行しません。

 

 





