---
title: デバイスの D3cold 機能
description: デバイスの電源ポリシー所有者 (PPO) であるドライバーがデバイスを D3cold に入力できるようにするには (コンピューターが S0 のままになっている場合)、ドライバーはデバイスの応答性が高く、デバイスが D3cold に入った後も正常に動作し続けることを確認する必要があります。
ms.assetid: 5A6CB076-7D97-48EC-B2BF-3204CD093B3E
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4d89053138d87abd38e2a6b555c65f4f4c6fb819
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828437"
---
# <a name="d3cold-capabilities-of-a-device"></a>デバイスの D3cold 機能


デバイスの電源ポリシー所有者 (PPO) であるドライバーがデバイスを D3cold に入力できるようにするには (コンピューターが S0 のままになっている場合)、ドライバーはデバイスの応答性が高く、デバイスが D3cold に入った後も正常に動作し続けることを確認する必要があります。

プラグアンドプレイ (PnP) デバイスの場合、オペレーティングシステムは通常、親バスドライバーからデバイスの D3cold 機能に関する情報を取得します。

たとえば、デバイスが PCI または PCI Express バスに接続されている場合、デバイスの PCI 構成領域には、デバイスの機能を示す電源管理レジスタブロックが含まれます。 このブロックの機能フラグは、デバイスが電源管理イベントまたは PME (wake イベントの PCI 用語) を通知できるデバイスの電源状態を指定します。 これらの状態には、D3hot と D3cold が含まれる場合があります。 PCI 電源管理の詳細については、 [Pci バス電源管理インターフェイスの仕様](https://pcisig.com/specifications/conventional/pci_bus_power_management_interface/)を参照してください。

デバイスが、入力された低電力の Dx 状態からウェイクアップイベントを通知できる必要がある場合、デバイス、親バスコントローラー、およびハードウェアプラットフォームが D3cold からの wake イベントの通知をサポートしていない限り、デバイスは D3cold に入ってはなりません。

デバイスの KMDF ドライバーは、 [**WdfDeviceAssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)メソッドを呼び出して、デバイスがウェイクアップイベントを通知できる最も低い電力状態でデバイスをアイドル状態にします。 KMDF バージョン1.11 以降、 **WdfDeviceAssignS0IdleSettings**には、可能な低電力の Dx 状態の範囲の D3cold が含まれています。 この方法では、デバイス、親バスドライバー、および ACPI システムファームウェアが D3cold からの wake イベントのシグナリングをサポートしている場合にのみ、D3cold でデバイスをアイドル状態にすることができます。

デバイスの WDM ドライバーは、デバイスがアイドル状態のときにデバイスの移動先となる低電力の Dx 状態を決定する必要があります。 (これに対して、 **WdfDeviceAssignS0IdleSettings**は、ドライバーが必要としないように、この Dx 状態を自動的に選択します)。デバイスが、入力された低電力の Dx 状態からウェイクアップイベントを通知できる必要がある場合、ドライバーは[*GetIdleWakeInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-get_idle_wake_info)ルーチンを呼び出して、デバイスがウェイクアップイベントを通知できる最も低い電源装置の電源状態を判断できます。 この情報を取得するために、 *GetIdleWakeInfo*は基になるバスドライバーと ACPI システムファームウェアを照会します。 *GetIdleWakeInfo*からの情報に基づいて、ドライバーは[*SetD3ColdSupport*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-set_d3cold_support)ルーチンを呼び出して、デバイスの D3cold への移行を有効または無効にすることができます。

デバイスは、D3cold からのウェイクイベントを通知する機能を必要としない場合があります。 デバイスは、ソフトウェアによって開始されるアクションに応答して、D3cold から D0 への移行のみを行う必要がある場合があります。 たとえば、ドライバーがデバイスの i/o 要求を受け取った場合、ドライバーはデバイスのスリープ解除を必要とすることがあります。 いくつかの例外を除き、このようなデバイスのドライバーによって、デバイスで D3cold を入力できるようになります。 例外として、D3cold から D0 への移行を実行するのに長時間かかるデバイスが考えられます。 たとえば、ディスプレイデバイスに大量のメモリが含まれていて、デバイスが D3cold に入ってから、デバイスが D3cold を終了した後に復元される必要がある場合があります。

D3cold の ACPI サポートの詳細については、「 [D3cold のファームウェアの要件](https://docs.microsoft.com/windows-hardware/drivers/bringup/firmware-requirements-for-d3cold)」を参照してください。

 

 




