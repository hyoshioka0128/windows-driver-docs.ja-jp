---
title: 予期しないウェイクアップ
description: 突然のウェイクアップは、D0 への予期しない移行です。
ms.assetid: 07D3EC05-A1C9-40C5-90FC-E25B5A66B064
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1bd9edda3dea9c2b94ccf14bbb3d832664470ba7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836185"
---
# <a name="surprise-wake-up"></a>予期しないウェイクアップ


突然のウェイクアップは、D0 への予期しない移行です。 デバイスが D3cold になると、同じ電源レール上の別のデバイスのドライバーが D3cold から D0 への移行を要求したときの副作用として、突然ウェイクアップが発生する可能性があります。 最初のデバイスのドライバーは、デバイスが初期化されていない D0 状態のままにならないように、突然ウェイクアップの通知を受け取る必要があります。

デバイスが D3hot から D3cold に移動した場合、他のいくつかのデバイスと共有する電源がオフになっていることが原因であると考えられます。 これらのデバイスが D3cold になると、あるデバイスのドライバーが D0 への移行を要求することがあります。 この要求に応答して、親バスドライバーまたは ACPI フィルタードライバーによって電源がオンになり、電源を共有するすべてのデバイスに既定の電源オンハードウェアの状態が入力されます。

この電力状態の変更を想定しているデバイスドライバーは、変更を要求したドライバーだけです。 他のデバイスのドライバーは、この変更の通知を受信する必要があります。これにより、D0 で動作するようにデバイスを正しく初期化できます。 この通知を受信できるドライバーだけが、そのデバイスで D3cold を入力できるようにする必要があります。 そうしないと、デバイスが D0 に入るタイミングがドライバーによって認識されません。

デバイスの電源をオンにすると、既定の初期化されていないハードウェアの状態が入力されます。 たとえば、 [PCI Express Base 3.0 仕様](https://pcisig.com/specifications/pciexpress/specifications/)では、デバイスが最初に電源を供給するときに入力する、*未初期化*状態を定義しています。 この状態の定義は PCI および PCI Express デバイスに固有ですが、他のバスに接続するデバイスは、電源が入っているときに同様のハードウェア状態を入力するように設計されています。

複数の機能を実装する PCI または PCI Express デバイスの場合、これらのデバイス関数は同じ電源レールを共有することがあります。 ただし、各関数は個別のドライバーを持つことができ、これらの関数のドライバーは相互に直接通信することはほとんどありません。 これらの関数のいずれかのドライバーが電源状態の変更を D3cold から D0 に要求した場合、他の関数のドライバーはこの変更を想定していません。 これらの他の関数が電力を受け取ると、そのドライバーは、D0 で正しく動作するように機能を構成できるように通知される必要があります。

バスドライバーは、子デバイスの電源がオンになっていることを検出します。 このデバイスの関数ドライバーが D0 への移行を要求しなかった場合、バスドライバーはデバイスドライバーに対して、D0 電源 IRP を送信するように要求します ( [**IRP\_\_設定**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)されている\_電源要求をターゲット状態 = **PowerDeviceD0**) を初期化します。D0 で動作するデバイス。 この初期化された D0 状態から、デバイスドライバーはデバイスの D3hot への移行を開始できます。 デバイスドライバーは、次の方法でバスドライバーから D0 への突然の移行通知を受け取ることができます。

-   [ランタイム電源管理フレームワーク](overview-of-the-power-management-framework.md)(pofx) のクライアントとして直接または間接的に登録するデバイスドライバーは、通知コールバックを受信します。
-   デバイスのスリープ状態を arm に設定するデバイスのドライバーは、バスドライバーによって完了した[ **\_のウェイク要求\_待機**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)して保留中の IRP\_します。

Windows 8 以降では、電源ポリシー所有者として機能するデバイスの関数ドライバーは、PoFx のクライアントとして登録できます。 バスドライバーは、デバイスが D0 への突然の移行を経験したことを PoFx に通知するときに、デバイスが初期化された D0 状態に移行してから、D3hot に通知するのに役立ちます。 まず、PoFx はドライバーの[*Devicepowerrequiredcallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_device_power_required_callback)ルーチンを呼び出して、デバイスドライバーに対して D0 power IRP をデバイススタックに送信するように要求します。 次に、PoFx はドライバーの[*Devicepowernotrequiredcallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_device_power_not_required_callback)ルーチンを呼び出して、デバイスが D0 状態のままである必要がないことをデバイスドライバーに通知します。

カーネルモードドライバーフレームワーク (KMDF) バージョン1.11 以降では、単一コンポーネントデバイス用の KMDF ドライバーは、 [**Wdfdevicewdm割り当て Powerframeworksettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmassignpowerframeworksettings)メソッドを呼び出すことによって、それ自体を pofx に間接的に登録できます。 この呼び出しでは、ドライバーは、予期しないのが D0 に移行したことをドライバーに通知するコールバックルーチンへのポインターを提供します。 詳細については、「[機能の電源状態のサポート](https://docs.microsoft.com/windows-hardware/drivers/wdf/supporting-functional-power-states)」を参照してください。

デバイスがウェイクアップ用に設定されている場合、PoFx にデバイスを登録していないドライバーにも、D0 への突然の移行が通知される可能性があります。 バスドライバーはデバイスの電源をオンにすると、ドライバーの**IRP\_完了\_待機\_ウェイク**要求を完了します。 応答として、ドライバーは、D0 で動作するようにデバイスを初期化します。 デバイスがアイドル状態になっている可能性があります。この場合、ドライバーはしばらくすると、このデバイスを D3hot に移動します。

PoFx に登録されておらず、デバイスをウェイクアップ用に arm していない関数ドライバーは、D3cold から D0 への突然の移行に関する通知を受け取りません。 デバイスは、初期化されていない D0 状態で大量の時間を消費する可能性があります。 この状態では、通常、デバイス内のすべてのコンポーネントがオンになっています。 アイドル状態のデバイスによる電力消費を減らすために、ドライバーは、D0 への突然の遷移の通知を受信できる場合にのみ、D3cold にエントリを有効にする必要があります。

 

 




