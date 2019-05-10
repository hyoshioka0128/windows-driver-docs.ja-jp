---
title: デバイスの D3cold 機能
description: D3cold (コンピューターの S0 内に存続するとき) を入力するデバイスは、デバイスの電源ポリシー所有者 (PPO) である、ドライバーは可能前に、ドライバーは、デバイスが応答および D3cold を入力すると、デバイスが正しく動作しているに確認する必要があります。
ms.assetid: 5A6CB076-7D97-48EC-B2BF-3204CD093B3E
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1dbcd8e09bdf314140ab810ccd2eabdba6c2b33e
ms.sourcegitcommit: 944535d8e00393531f6b265317a64da3567e4f2c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65106433"
---
# <a name="d3cold-capabilities-of-a-device"></a>デバイスの D3cold 機能


D3cold (コンピューターの S0 内に存続するとき) を入力するデバイスは、デバイスの電源ポリシー所有者 (PPO) である、ドライバーは可能前に、ドライバーは、デバイスが応答および D3cold を入力すると、デバイスが正しく動作しているに確認する必要があります。

プラグ アンド プレイ (PnP) デバイスのオペレーティング システムは通常親バス ドライバーから、デバイスの D3cold 機能に関する情報を取得します。

たとえば、デバイスが、PCI や PCI Express バスに接続されている場合、デバイスの PCI 構成領域には電源管理の登録とするブロック デバイスの機能を示すが含まれます。 このブロックで機能フラグは、電源管理イベント、または PME (ウェイク イベントの PCI 語句) をシグナル状態、デバイスをデバイスの電源状態を指定します。 これらの状態は、D3hot と D3cold などがあります。 PCI の電源管理の詳細については、次を参照してください。、 [PCI バス Power Management Interface Specification](https://www.pcisig.com/specifications/conventional/pci_bus_power_management_interface/)します。

デバイスが D3cold を入力しない場合は、デバイスは、それが入力する低電力 Dx 状態からウェイク イベントを通知できる必要があります、デバイス、親のバス コント ローラー、およびハードウェア プラットフォーム D3cold からウェイク イベントをシグナル通知をサポートしない限り、します。

デバイスの KMDF ドライバーは呼び出し、 [ **WdfDeviceAssignS0IdleSettings** ](https://msdn.microsoft.com/library/windows/hardware/ff545903)メソッド、デバイスが、ウェイク イベントを信号を利用した最下位のデバイスの電源状態でアイドル状態にデバイスを有効にします。 KMDF バージョン 1.11 以降**WdfDeviceAssignS0IdleSettings** D3cold には低電力 Dx 状態の範囲が含まれています。 このメソッドは、デバイス、デバイス、親のバス ドライバー、および ACPI システム ファームウェア D3cold からウェイク イベントをシグナル化をサポートしている場合にのみ、D3cold でアイドル状態にできます。

デバイスの WDM ドライバーには、デバイスがアイドル状態の場合、デバイスに移動する低電力 Dx 状態を決める必要があります。 (これに対し、 **WdfDeviceAssignS0IdleSettings**ドライバーがする必要があるないように、この Dx 状態を自動的に選択します)。ドライバーを呼び出すことができる場合、デバイスは、それが入力する低電力 Dx 状態からウェイク イベントを通知できる必要があります、 [ *GetIdleWakeInfo* ](https://msdn.microsoft.com/library/windows/hardware/hh967712)元となる最小搭載デバイスの電源状態を確認するルーチンデバイスは、ウェイク イベントを通知できます。 この情報を取得する*GetIdleWakeInfo*バス ドライバーの基になると ACPI システム ファームウェア クエリを実行します。 情報に基づき*GetIdleWakeInfo*、ドライバーを呼び出すことができます、 [ *SetD3ColdSupport* ](https://msdn.microsoft.com/library/windows/hardware/hh967716)ルーチンを有効または D3cold にデバイスの移行を無効にします。

デバイスでは、D3cold からウェイク イベントを通知する機能は必要はありません。 代わりに、デバイスはソフトウェアによって開始された操作に対する応答としてのみ D3cold から D0 への移行を行うに必要な場合があります。 たとえば、ドライバーは、ドライバー、デバイスの I/O 要求を受信する場合、デバイスのスリープを解除する必要があります。 いくつかの例外を除き、このようなデバイスのドライバーが D3cold を入力するデバイスを有効にできます。 可能性のある例外は、大量の D0 に D3cold から移行する時間を必要とするデバイスです。 たとえば、ディスプレイ デバイスには、大量デバイス D3cold に入る前に保存して、デバイスが D3cold が終了した後に復元する必要があるメモリにはが含まれます。

D3cold の ACPI サポートの詳細については、次を参照してください。 [D3cold のファームウェア要件](https://msdn.microsoft.com/library/windows/hardware/dn605829)します。

 

 




