---
title: デバイス稼働状態 D0
description: デバイス稼働状態 D0
ms.assetid: 6b0ec03a-eaf1-4c96-aaae-dfe821583787
keywords:
- デバイスの電源状態の WDK カーネル
- Dx 名 WDK の電源管理
- デバイスの状態の WDK 電源管理の操作
- 継続的な電源 WDK カーネル
- WDK の遅延の電源管理
- 作業の状態の WDK 電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b7457fd6a4cd782d70a53b51c84a818ec521d6f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385002"
---
# <a name="device-working-state-d0"></a>デバイス稼働状態 D0





D0 デバイスの電源状態では、デバイスが完全に操作可能な状態です。 この状態で、デバイス ドライバーは、I/O 操作を実行するデバイスと対話でき、デバイスの割り込みを生成します。 デバイスのメモリまたは I/O のアドレス空間にマップされているハードウェア レジスタの場合、ドライバーはこれらのレジスタにアクセスできます。

Windows 8 以降では、デバイス ドライバーが接続できる、[パッシブ レベル割り込みサービス ルーチン](using-passive-level-interrupt-handling-routines.md)(ISR) デバイスからの割り込みにします。 デバイスは、D0 内にあるかどうかに関係なく割り込みを生成できます。 デバイスは、低電力 Dx 状態のときに、D0 に戻す、デバイスに、トリガーとして機能する割り込みを生成できます。 IRQL で実行がスケジュールされる ISR = パッシブ\_D0 を入力すると、デバイス レベルします。 などの Windows 7、Windows の以前のバージョン D0 以外のデバイスの電源状態にあるときに割り込みの場所をデバイスが発生しない必要があります。

D0 から低電力 Dx 状態への移行ののみ、デバイス ドライバー、デバイスの電源ポリシーの所有者として動作しているを開始した場合、移行の呼び出しが発生する可能性が、 [ **PoRequestPowerIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-porequestpowerirp)ルーチンです。 電源 IRP を送信する電源マネージャーをこの呼び出しに応答すると ([**IRP\_MN\_設定\_POWER**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power))、デバイス ドライバー、バス ドライバー、およびプラットフォームファームウェア (を通じて、 [ACPI の Windows ドライバー](acpi-driver.md)Acpi.sys) デバイスの電源状態を変更するには、この IRP を協調的に処理します。

通常、デバイスのハードウェアは、一連のいずれかの実行時の割り込みを発生したり、デバイスの構成方法に応じて、シグナルをスリープ解除を内部イベントを監視します。 ドライバーは、ウェイク イベントに応答して、割り込みに応答するコード パスを 1 つを実装します。 割り込みのコード パスが、ウェイク イベントを処理する必要はありませんし、ウェイク アップのコード パスは、割り込みを処理する必要はありませんがある場合、ドライバーのコードを簡略化できます。 ベスト プラクティスとしては、ドライバーは、デバイスが、D0 場合にのみ、割り込みを生成して、デバイスが Dx 低電力状態になっている場合にのみ、ウェイク信号を生成するデバイスを構成する必要があります。 通常、ドライバーは、直前に、デバイスが、D0 を終了し、デバイスが D0 直後後に割り込みを生成するデバイスを構成しますウェイク信号を生成するデバイスを構成します。

通常、デバイスのハードウェア リセット シグナルがアサートされたときに D0 状態になります。 実際には、PCI や PCI Express などのバスの仕様では、この動作が必要です。

D0 状態の特性を次に示します。

<a href="" id="power-consumption"></a>**電力消費量**  
デバイスの継続的な電力消費の最高レベルです。

<a href="" id="device-context"></a>**デバイス コンテキスト**  
すべてのコンテキストが保持されます。

<a href="" id="device-driver-behavior"></a>**デバイス ドライバーの動作**  
通常の操作。

<a href="" id="restore-time"></a>**復元時間**  
適用できません。

<a href="" id="wake-up-capability"></a>**ウェイク アップ機能**  
適用できません。

 

 




