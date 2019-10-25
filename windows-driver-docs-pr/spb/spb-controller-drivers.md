---
title: SPB コントローラードライバー
description: SPB コントローラーは、単純な周辺機器バス (SPB) を制御し、SPB に接続されている周辺機器との間でデータを転送するデバイスです。
ms.assetid: 046353F9-315F-4328-8ECA-1C23AF87B4B4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d3ef84a7c783cc3b80e75aeacf7b44b17a030e6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839630"
---
# <a name="spb-controller-drivers"></a>SPB コントローラードライバー


SPB コントローラーは、[単純な周辺機器バス](https://docs.microsoft.com/previous-versions/hh450903(v=vs.85))(spb) を制御し、spb に接続されている周辺機器との間でデータを転送するデバイスです。 SPB コントローラーのハードウェアベンダーは、コントローラーのハードウェア機能を管理する SPB コントローラードライバーを提供します。

Windows 8 以降では、SPB フレームワーク拡張 (SpbCx) により、[シンプルな周辺機器](https://docs.microsoft.com/previous-versions/hh450903(v=vs.85))(spb) のコントローラードライバーの開発が簡素化されています。 SpbCx は、システムによって提供される[カーネルモードドライバーフレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/what-s-new-for-wdf-drivers)(kmdf) の拡張機能です。 SPB コントローラーデバイスのハードウェアベンダーは、すべてのハードウェア固有のドライバー操作を実行するコントローラードライバーを提供します。 このドライバーは、SPB コントローラーに固有の操作を実行するために SpbCx と通信し、KMDF と直接通信して汎用ドライバー操作を実行します。

たとえば、SPB コントローラードライバーは、通常、KMDF の[**WdfDeviceInitSetPnpPowerEventCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpnppowereventcallbacks)メソッドを呼び出して、power イベントコールバックを受信するように登録し、 [**WdfInterruptCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptcreate)メソッドを呼び出してドライバーの割り込みを接続します。SPB コントローラーからの割り込みまでのサービスルーチン (ISR)。 Spb コントローラーは、sp 固有の操作を実行するために、spbcx [device driver interface](https://docs.microsoft.com/previous-versions/hh698219(v=vs.85)) (DDI) を介して spbcx と通信します。

Spbcx と連携し、SPB に接続されている周辺機器の i/o 要求を処理するために、SBP controller ドライバーで動作します。 SpbCx は、SPB コントローラードライバーに共通する処理タスクを実行します。 これらのタスクには、SPB コントローラーの i/o 要求キューの管理が含まれます。 これらのキューには、バスに接続されている周辺機器を管理するドライバーからの i/o 要求が含まれています。 SPB コントローラードライバーは、これらの要求を処理するために必要なハードウェア固有の操作をすべて実行します。

次の図は、SPB コントローラードライバーと SpbCx を示しています。

![spb コンポーネントのブロック図](images/spbmodules.png)

SPB コントローラードライバーと SpbCx はどちらもカーネルモードで動作し、SpbCx DDI を介して相互に通信します。 SPB コントローラードライバーは、SpbCx によって実装されたドライバーサポートメソッドを呼び出します。 SpbCx は、SPB コントローラードライバーによって実装されるイベントコールバック関数を呼び出します。

SPB コントローラーに i/o 要求を送信するドライバーは、[カーネルモードドライバーフレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/what-s-new-for-wdf-drivers)(kmdf) を使用するカーネルモードドライバーか、[ユーザーモードドライバーフレームワーク](https://docs.microsoft.com/previous-versions/ff554928(v=vs.85))(UMDF) を使用するユーザーモードドライバーのいずれかです。 これらのドライバーは、SPB に接続されている周辺機器との間でデータを転送するために、読み取り要求と書き込み要求を送信できます。 さらに、ドライバーは、SPB 固有の操作を実行するために i/o 制御 (IOCTL) 要求を送信できます。

Spb コントローラードライバーは、spb コントローラーデバイスのハードウェアレジスタに直接アクセスして、SPB に接続されている周辺機器との間のデータ転送を開始します。 I ² C などの SPB の場合、これらのデータ転送は比較的低速な速度で行われます。 SPB コントローラーのハードウェアレジスタはメモリにマップされている可能性がありますが、周辺機器の登録には SPB 経由で順次アクセスする必要があります。

SPB 接続周辺機器との間でデータを転送する i/o 要求に応答して、SPB コントローラードライバーはバス転送を開始し、i/o 要求を保留中としてマークし、転送が完了するのを待たずに制御を戻します。 その後、SPB コントローラーハードウェアが転送を完了すると、コントローラーは割り込みを通知し、SPB コントローラードライバーの ISR は保留中の i/o 要求を完了するか、要求された i/o 操作で次の転送を開始します。

I/o 要求を直接 SPB コントローラーに送信できるのは、ドライバーだけです。 ユーザーモードアプリケーションが SPB に接続されている周辺機器との間でデータを転送する場合、アプリケーションは spb 周辺機器ドライバーに依存して、対応する読み取り要求または書き込み要求を SPB コントローラーに送信する必要があります。

## <a name="in-this-section"></a>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>トピック</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/spb/spb-framework-extension" data-raw-source="[SPB Framework Extension (SpbCx)](https://docs.microsoft.com/windows-hardware/drivers/spb/spb-framework-extension)">SPB フレームワーク拡張機能 (SpbCx)</a></p></td>
<td><p>Windows 8 以降では、SPB framework extension (SpbCx) は、<a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/what-s-new-for-wdf-drivers" data-raw-source="[Kernel-Mode Driver Framework](https://docs.microsoft.com/windows-hardware/drivers/wdf/what-s-new-for-wdf-drivers)">カーネルモードドライバーフレームワーク</a>(kmdf) のシステム提供の拡張機能です。 SpbCx は、 <a href="https://docs.microsoft.com/previous-versions/hh698221(v=vs.85)" data-raw-source="[SPB controller driver](https://docs.microsoft.com/previous-versions/hh698221(v=vs.85))">spb コントローラードライバー</a>と連携して、i ² C や SPI など、<a href="https://docs.microsoft.com/previous-versions/hh450903(v=vs.85)" data-raw-source="[simple peripheral bus](https://docs.microsoft.com/previous-versions/hh450903(v=vs.85))">単純な周辺機器バス</a>(SPB) に接続されている周辺機器に i/o 操作を実行します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/spb/spbcx-interfaces" data-raw-source="[SpbCx Interfaces](https://docs.microsoft.com/windows-hardware/drivers/spb/spbcx-interfaces)">SpbCx インターフェイス</a></p></td>
<td><p>SPB framework extension (SpbCx) には、2つのインターフェイスがあります。 1つは、SPB コントローラーのクライアント (周辺ドライバー) がバスに接続されている周辺機器に送信する i/o 要求を SpbCx が受け入れる i/o 要求インターフェイスです。 2番目のインターフェイスは、SpbCx が SPB コントローラードライバーと通信するデバイスドライバーインターフェイス (DDI) です。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/spb/i-o-transfer-sequences" data-raw-source="[I/O Transfer Sequences](https://docs.microsoft.com/windows-hardware/drivers/spb/i-o-transfer-sequences)">I/o 転送シーケンス</a></p></td>
<td><p>SPB framework extension (SpbCx) では、i/o 転送シーケンスがサポートされています。 I/o 転送シーケンスは、単一のアトミックバス操作として実行される、順序付けされたバス転送 (読み取りおよび書き込み操作) のセットです。 I/o 転送シーケンス内のすべての転送は、バス上の同じターゲットデバイスにアクセスします。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/spb/handling-client-implemented-sequences" data-raw-source="[Handling Client-Implemented Sequences](https://docs.microsoft.com/windows-hardware/drivers/spb/handling-client-implemented-sequences)">クライアントによって実装されたシーケンスの処理</a></p></td>
<td><p>省略可能な<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_controller_lock" data-raw-source="[&lt;em&gt;EvtSpbControllerLock&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_controller_lock)"><em>evtspbコントローラー</em></a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_controller_unlock" data-raw-source="[&lt;em&gt;EvtSpbControllerUnlock&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_controller_unlock)"><em>evtspbコントローラーの unlock</em></a>イベントコールバック関数は、補完的な操作を実行します。 <em>Evtspbコントローラーロック</em>関数は、 <a href="https://msdn.microsoft.com/library/windows/hardware/hh450858" data-raw-source="[&lt;strong&gt;IOCTL_SPB_LOCK_CONTROLLER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh450858)"><strong>IOCTL_SPB_LOCK_CONTROLLER</strong></a>要求のハンドラーです。 <em>Evtspbコントローラーロック解除</em>関数は、 <a href="https://msdn.microsoft.com/library/windows/hardware/hh450859" data-raw-source="[&lt;strong&gt;IOCTL_SPB_UNLOCK_CONTROLLER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh450859)"><strong>IOCTL_SPB_UNLOCK_CONTROLLER</strong></a>要求のハンドラーです。 クライアント (つまり、バス上の周辺機器のドライバー) は、これらの要求を開始および終了<a href="https://docs.microsoft.com/windows-hardware/drivers/spb/i-o-transfer-sequences" data-raw-source="[I/O transfer sequences](https://docs.microsoft.com/windows-hardware/drivers/spb/i-o-transfer-sequences)">i/o 転送シーケンス</a>に送信します。 ほとんどの SPB コントローラードライバーは、 <strong>IOCTL_SPB_LOCK_CONTROLLER</strong>および<strong>IOCTL_SPB_UNLOCK_CONTROLLER</strong>要求をサポートしていないため、 <em>evtspbcontroller ロック</em>関数と<em>evtsp UNLOCK</em>関数は実装しません。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/spb/using-the-spb-transfer-list-structure" data-raw-source="[Using the SPB_TRANSFER_LIST Structure for Custom IOCTLs](https://docs.microsoft.com/windows-hardware/drivers/spb/using-the-spb-transfer-list-structure)">カスタム Ioctl に SPB_TRANSFER_LIST 構造を使用する</a></p></td>
<td><p>シンプルな周辺機器バス (SPB) コントローラードライバーで1つ以上のカスタム i/o 制御 (IOCTL) 要求がサポートされている場合は、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/spb/ns-spb-spb_transfer_list" data-raw-source="[&lt;strong&gt;SPB_TRANSFER_LIST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/spb/ns-spb-spb_transfer_list)"><strong>SPB_TRANSFER_LIST</strong></a>構造体を使用して、これらの要求の読み取りバッファーと書き込みバッファーを記述します。 この構造体は、要求内のバッファーを記述するための統一された方法を提供し、METHOD_BUFFERED i/o 操作に関連するバッファーコピーオーバーヘッドを回避します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/spb/handling-ioctl-spb-full-duplex-requests" data-raw-source="[Handling IOCTL_SPB_FULL_DUPLEX Requests](https://docs.microsoft.com/windows-hardware/drivers/spb/handling-ioctl-spb-full-duplex-requests)">IOCTL_SPB_FULL_DUPLEX 要求の処理</a></p></td>
<td><p>SPI などの一部のバスでは、バスコントローラーとバス上のデバイスの間で同時に読み取りと書き込みの転送を行うことができます。 これらの全二重転送をサポートするために、シンプルな周辺機器バス (SPB) i/o 要求インターフェイスの定義には、オプションとして<a href="https://msdn.microsoft.com/library/windows/hardware/hh974774" data-raw-source="[&lt;strong&gt;IOCTL_SPB_FULL_DUPLEX&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh974774)"><strong>IOCTL_SPB_FULL_DUPLEX</strong></a> i/o 制御コード (IOCTL) が含まれています。 <strong>IOCTL_SPB_FULL_DUPLEX</strong> IOCTL をサポートする必要があるのは、ハードウェアで全二重転送を実装するバスコントローラーの SPB コントローラードライバーだけです。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/spb/how-to-get-the-connection-settings-for-a-device" data-raw-source="[How to Get the Connection Settings for a Device](https://docs.microsoft.com/windows-hardware/drivers/spb/how-to-get-the-connection-settings-for-a-device)">デバイスの接続設定を取得する方法</a></p></td>
<td><p>SPB コントローラードライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_target_connect" data-raw-source="[&lt;em&gt;EvtSpbTargetConnect&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_target_connect)"><em>Evtspbtargetconnect</em></a>コールバック関数を登録した場合、この<a href="https://docs.microsoft.com/windows-hardware/drivers/spb/spb-framework-extension" data-raw-source="[SPB framework extension](https://docs.microsoft.com/windows-hardware/drivers/spb/spb-framework-extension)">関数は、</a>コントローラーのクライアント (周辺ドライバー) がを開くために<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create" data-raw-source="[&lt;strong&gt;IRP_MJ_CREATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)"><strong>IRP_MJ_CREATE</strong></a>要求を送信したときに、この関数を呼び出します。バス上のターゲットデバイスへの論理接続。 <em>Evtspbtargetconnect</em>コールバックへの応答として、SPB コントローラードライバーは、ターゲットデバイスの接続設定を取得するために、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nf-spbcx-spbtargetgetconnectionparameters" data-raw-source="[&lt;strong&gt;SpbTargetGetConnectionParameters&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nf-spbcx-spbtargetgetconnectionparameters)"><strong>Spbtargetgetconnectionparameters</strong></a>メソッドを呼び出す必要があります。 SPB コントローラードライバーはこれらの設定を保存し、後でクライアントからの i/o 要求に応答してデバイスにアクセスするために使用します。</p></td>
</tr>
</tbody>
</table>

 

 

 




