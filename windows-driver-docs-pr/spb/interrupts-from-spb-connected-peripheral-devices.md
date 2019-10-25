---
title: SPB に接続されている周辺機器からの割り込み
description: PCI などのバスとは異なり、I ² C や SPI などの単純な周辺機器バス (SPB) は、周辺機器からプロセッサに割り込み要求を伝達するための標準のバス固有の手段を提供しません。
ms.assetid: E302BB21-582E-494E-9ADD-72703EF32446
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2944a62136b187f84aa0e3f916c6de3297d2e601
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839636"
---
# <a name="interrupts-from-spb-connected-peripheral-devices"></a>SPB に接続されている周辺機器からの割り込み


PCI などのバスとは異なり、I ² C や SPI などの[単純な周辺機器バス](https://docs.microsoft.com/previous-versions/hh450903(v=vs.85))(SPB) は、周辺機器からプロセッサに割り込み要求を伝達するための標準のバス固有の手段を提供しません。 代わりに、SPB に接続されている周辺機器は、SPB と SPB の両方のコントローラーの外部にある別のハードウェアパスを使用して割り込みを通知します。 この割り込みパスの詳細は、ハードウェアプラットフォームによって異なりますが、Windows では、SPB に接続されている周辺機器のドライバーからこれらの詳細を非表示にして、ドライバーがさまざまなハードウェアプラットフォームで動作できるようにします。




通常、SPB に接続されている周辺機器の割り込み要求ラインは、汎用 i/o (GPIO) コントローラーのピンに接続され、GPIO コントローラーはデバイスからプロセッサに割り込みをリレーします。 詳細については、「 [GPIO 割り込み](https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-interrupts)」を参照してください。

周辺機器ドライバーは、この GPIO 割り込みを抽象 Windows interrupt リソース (**Cmresourcetypeinterrupt**) として取得し、割り込みをドライバーの interrupt service ルーチン (ISR) に接続します。 割り込みリソースの抽象化は、ドライバーからの割り込みのプラットフォーム固有の詳細を非表示にします。 たとえば、ドライバーは、割り込みを GPIO ピンから受け取るか、他のソースから受信するかなどの詳細を無視できます。 この抽象化を維持するために、DIRQL で実行されるカーネルの割り込みトラップハンドラーは、GPIO pin で割り込みをクリアするか一時的にマスクすることによって、アクティブな割り込み要求をサイレント状態にする必要がある場合があります。 通常、GPIO コントローラーのハードウェアレジスタはメモリにマップされ、DIRQL でアクセスできます。

これに対して、SPB に接続されている周辺機器はメモリにマップされていないため、このデバイスの ISR は通常、IRQL = パッシブ\_レベルで実行する必要があります。 デバイス内のハードウェアレジスタにアクセスするために、ISR は i/o 要求を送信して SPB での直列転送を実行します。 このような転送は比較的低速で、DIRQL で実行される ISR では実行できません。 ただし、パッシブレベルの ISR は、i/o 要求を同期的に送信し、要求が完了するまでブロックすることができます。

エッジによってトリガーされる割り込みの場合、カーネルのトラップハンドラーによって、GPIO ピンで割り込み要求が自動的にクリアされ、デバイスの ISR がパッシブレベルで実行されるようにスケジュールされます。 トラップハンドラーは、トラップハンドラーが返された後に、同じ割り込みが再度発生しないように、割り込みをクリアする必要があります。

レベルでトリガーされる割り込みでは、カーネルの割り込みトラップハンドラーによって、GPIO ピンで割り込み要求が自動的にマスクされ、デバイスの ISR がパッシブレベルで実行されるようにスケジュールされます。 ISR は、デバイスからの割り込み要求をクリアする必要があります。 ISR から制御が戻った後、カーネルは、GPIO ピンで割り込み要求をマスク解除します。

デバイスのパッシブレベルの ISR は、割り込みの初期サービスのみを実行してから、他のデバイスのパッシブレベルの Isr の遅延を避けるためにを返します。 通常、ドライバーは、ISR よりも低い優先順位で実行される割り込みワーカースレッドに対して、割り込みに関連する追加の処理を遅らせる必要があります。

Windows 8 以降では、[ユーザーモードドライバーフレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/overview-of-the-umdf)(umdf) は、umdf ドライバーの isr をサポートしています。 SPB 周辺機器の UMDF ドライバーは、 [**IWDFDevice3:: createinterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice3-createinterrupt)メソッドを呼び出して、デバイスからの割り込みに ISR を接続します。 デバイスが割り込み要求を通知すると、カーネルのトラップハンドラーによって、ISR がパッシブレベルで実行されるようにスケジュールされます。 詳細については、「[ハードウェアへのアクセスと割り込みの処理](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-hardware-and-handling-interrupts)」を参照してください。

Windows 8 以降では、[カーネルモードドライバーフレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/what-s-new-for-wdf-drivers)(kmdf) はパッシブレベルの isr をサポートしています。 SPB 周辺機器の KMDF ドライバーは、 [**WdfInterruptCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptcreate)メソッドを呼び出して、パッシブレベルの ISR をデバイスからの割り込みに接続します。 このメソッドの入力パラメーターの1つは、割り込みの構成情報を格納する[**WDF\_interrupt\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/ns-wdfinterrupt-_wdf_interrupt_config)構造体へのポインターです。 ISR がパッシブレベルで実行されるように構成するには、この構造体の "" の "設定のない**Veハンドリング**メンバーを**TRUE**に設定します。 詳細については、「[パッシブレベルの割り込みのサポート](https://docs.microsoft.com/windows-hardware/drivers/wdf/supporting-passive-level-interrupts)」を参照してください。

 

 




