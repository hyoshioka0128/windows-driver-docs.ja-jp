---
title: デバイス稼働状態 D0
description: デバイス稼働状態 D0
ms.assetid: 6b0ec03a-eaf1-4c96-aaae-dfe821583787
keywords:
- デバイスの電源状態 WDK カーネル
- Dx 名 WDK の電源管理
- デバイスの動作状態 WDK の電源管理
- 継続的なパワー WDK カーネル
- WDK 電源管理の遅延
- 作業状態 WDK の電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6783e4f03c64c4d490cd86eaf015fc9d21b0bd05
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836925"
---
# <a name="device-working-state-d0"></a>デバイス稼働状態 D0





デバイスのデバイスの電源状態は、デバイスが完全に動作し、操作可能であることを示します。 この状態では、デバイスドライバーはデバイスと対話して i/o 操作を実行でき、デバイスは割り込みを生成できます。 デバイスにメモリまたは i/o アドレス空間にマップされているハードウェアレジスタがある場合、ドライバーはこれらのレジスタにアクセスできます。

Windows 8 以降では、デバイスドライバーは、[パッシブレベルの割り込みサービスルーチン](using-passive-level-interrupt-handling-routines.md)(ISR) をデバイスからの割り込みに接続できます。 デバイスは、D0 にあるかどうかにかかわらず、割り込みを生成できます。 低電力の Dx 状態の場合、デバイスは、デバイスを D0 に戻すためのトリガーとして機能する割り込みを生成できます。 デバイスが D0 に入った後、ISR は IRQL = パッシブ\_レベルで実行するようにスケジュールされています。 Windows 7 を含め、以前のバージョンの Windows では、デバイスが D0 以外のデバイスの電源状態にある場合、割り込みを生成しないようにする必要があります。

D0 から低電力の Dx 状態への移行は、デバイスドライバーがデバイスの電源ポリシー所有者として動作しているときに、 [**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)ルーチンを呼び出すことによって遷移を開始する場合にのみ発生します。 Power IRP ([**irp\_\_セット\_電源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)) を送信することによってこの呼び出しに応答する場合、デバイスドライバー、バスドライバー、およびプラットフォームファームウェア ( [Windows ACPI ドライバー](acpi-driver.md)、acpi) の協調的ハンドルを使用します。この IRP は、デバイスの電源状態を変更します。

通常、デバイスハードウェアは、デバイスの構成方法に応じて、実行時の割り込みまたはウェイクシグナルを生成できる内部イベントのセットを監視します。 ドライバーは、割り込みに応答するための1つのコードパスと、ウェイクアップイベントに応答するためのコードパスを実装します。 割り込みコードパスでウェイクアップイベントを処理する必要がなく、ウェイクコードパスで割り込みを処理する必要がない場合は、ドライバーコードを簡略化できます。 ベストプラクティスとして、ドライバーは、デバイスが D0 にある場合にのみ割り込みを生成するようにデバイスを構成し、デバイスが低電力の Dx 状態にある場合にのみ wake 信号を生成するようにします。 通常、ドライバーはデバイスが D0 を終了する直前にウェイクアップ信号を生成するようにデバイスを構成し、デバイスが D0 に入った直後に割り込みを生成するようにデバイスを構成します。

通常、デバイスは、ハードウェアリセットシグナルがアサートされると、D0 状態になります。 実際、PCI や PCI Express などのバスの仕様では、この動作が必要になります。

次に、D0 状態の特性を示します。

<a href="" id="power-consumption"></a>**電力消費**  
デバイスの最高レベルの継続的な電力消費量。

<a href="" id="device-context"></a>**デバイスコンテキスト**  
すべてのコンテキストが保持されます。

<a href="" id="device-driver-behavior"></a>**デバイスドライバーの動作**  
通常の操作です。

<a href="" id="restore-time"></a>**復元時間**  
適用できません。

<a href="" id="wake-up-capability"></a>**ウェイクアップ機能**  
適用できません。

 

 




