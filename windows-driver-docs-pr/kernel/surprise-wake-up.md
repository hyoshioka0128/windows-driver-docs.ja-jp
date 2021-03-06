---
title: 予期しないウェイクアップ
description: 驚きのウェイク アップでは、D0 に予期しない移行です。
ms.assetid: 07D3EC05-A1C9-40C5-90FC-E25B5A66B064
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4b777b1e0e48245596cece58b07e5359faa9c465
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385107"
---
# <a name="surprise-wake-up"></a>予期しないウェイクアップ


驚きのウェイク アップでは、D0 に予期しない移行です。 デバイス D3cold を入力すると、同じ power レール上の別のデバイスのドライバー D3cold から D0 への遷移を要求するときに副作用として突然のウェイク アップが発生があります。 最初のデバイス ドライバーは、デバイスが初期化されていない d0 に残っていることを防ぐために、突然のウェイク アップの通知を受け取る必要があります。

D3hot から D3cold にデバイスを移動、ときにおそらくはいくつかの他のデバイスと共有している電源がオフになっていたためです。 これらのデバイスの入力、D3cold 後しばらくして、デバイスのいずれかのドライバーは D0 への移行を要求する可能性があります。 この要求に応答して、親バス ドライバーまたは ACPI フィルター ドライバーは、電源をオンにし、電源を共有するすべてのデバイスは、ハードウェアの電源の状態が既定を入力してください。

この電源状態の変更が必要とする唯一のデバイス ドライバーは、変更を要求したドライバーです。 その他のデバイス ドライバーは、D0 で動作するようにデバイスに正しく初期化できるように、この変更の通知を受け取る必要があります。 この通知を受け取ることができるドライバーのみに D3cold を入力するには、そのデバイスが有効にする必要があります。 それ以外の場合、ドライバーでは、デバイスが D0 に入ったときはわかりません。

デバイスがオンにすると、既定では、初期化されていないハードウェアの状態を入力します。 たとえば、 [PCI Express ベース 3.0 の仕様](https://pcisig.com/specifications/pciexpress/specifications/)を定義、 *D0 が初期化されていない*状態、デバイスは電源を最初に受信したときの入力をします。 この状態の定義は、PCI や PCI Express デバイスに固有ですが、他のバスに接続するデバイスが起動しているときのようなハードウェアの状態を入力するように設計します。

場合は複数の関数を実装する PCI や PCI Express デバイス、デバイスのこれらの関数はおそらく同じ電源レールを共有します。 ただし、各関数は、個別のドライバーを必要があります、これらの関数のドライバーは、互いに直接通信することはありません。 これらの関数のいずれかのドライバーでは、D0 に D3cold から電源状態の変更を要求、するとき、その他の関数のドライバーはこの変更を予期しません。 これらの機能は、電力を供給、D0 で正しく動作する関数を構成できるように、ドライバーに通知する必要があります。

子のデバイスに電源が入っているバス ドライバーを検出します。 バス ドライバーが D0 power IRP 自体を送信するデバイス ドライバーを求めるこのデバイスの機能のドライバーが D0 への遷移を要求していない場合 (、 [ **IRP\_MN\_設定\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)対象の状態を含む要求 = **PowerDeviceD0**) D0 で動作するデバイスを初期化します。 初期化されたこの D0 状態から、デバイス ドライバーは、D3hot へのデバイスの移行を開始できます。 デバイス ドライバー通知を受信できる突然遷移の D0 にバス ドライバーから次の方法で。

-   直接または間接的のクライアントとして自身を登録するデバイス ドライバー、[実行時の電源管理フレームワーク](overview-of-the-power-management-framework.md)(PoFx) 通知のコールバックを受信します。
-   スリープ解除するデバイスを arm デバイス用のドライバーが、保留中[ **IRP\_MN\_待機\_WAKE** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)バス ドライバーによって完了した要求。

Windows 8 以降、電源ポリシーの所有者として機能する、デバイスの機能のドライバーとして登録できます自体の PoFx クライアント。 バス ドライバーは、デバイスに D0 への突然の遷移が発生したことを PoFx に通知をするときに、デバイスに移動し、次を D0 の状態に初期化された D3hot が PoFx に役立ちます。 PoFx、まず、呼び出し、ドライバーの[ *DevicePowerRequiredCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_device_power_required_callback)ルーチンをデバイス スタック D0 電源 IRP を送信するデバイス ドライバを確認します。 次に、ドライバーの呼び出す PoFx [ *DevicePowerNotRequiredCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_device_power_not_required_callback) D0 状態を維持するためにデバイスがいないデバイス ドライバーに通知するルーチンが必要です。

単一コンポーネントのデバイスは直接いない自体が登録 PoFx 呼び出すことによって、カーネル モード ドライバー フレームワーク (KMDF) バージョン 1.11、KMDF ドライバーを開始、 [ **WdfDeviceWdmAssignPowerFrameworkSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicewdmassignpowerframeworksettings)メソッド。 この呼び出しでは、ドライバーは、D0 への突然の遷移のドライバーに通知するコールバック ルーチンへのポインターを提供します。 詳細については、次を参照してください。[サポート機能の電力状態](https://docs.microsoft.com/windows-hardware/drivers/wdf/supporting-functional-power-states)します。

PoFx でそのデバイスを登録できませんドライバーは、デバイスのスリープ解除されている場合、D0 への突然の遷移の通知も。 ドライバーのバス ドライバーは、デバイスの電源をオンにと、完了**IRP\_MN\_待機\_WAKE**要求。 応答では、ドライバーは、D0 で動作するには、そのデバイスを初期化します。 デバイスは、この場合、ドライバーでは、その後はこのデバイスに移動 D3hot、アイドル状態になる可能性があります。

関数のドライバー PoFx を登録しませんおよび、そのデバイスのスリープ解除を arm はない通知を受け取りますありません突然の切り替え効果の D3cold から D0 に。 デバイスは、初期化されていない d0 で大量の時間を費やす可能性があります。 この状態で、すべてのデバイスのコンポーネントが通常オンします。 をアイドル状態のデバイスでの電力消費量を削減するには、ドライバーは D0 への突然の遷移の通知を受信できる場合にのみ D3cold にエントリを有効する必要があります。

 

 




