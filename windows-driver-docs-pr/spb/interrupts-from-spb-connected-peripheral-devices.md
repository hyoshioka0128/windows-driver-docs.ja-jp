---
title: SPB 接続周辺機器からの割り込み
description: PCI などのバスとは異なり、I²C など SPI、シンプルな周辺機器バス (SPB) には周辺機器からすると、プロセッサの割り込み要求を伝達する標準化された、バスに固有の方法はありません。
ms.assetid: E302BB21-582E-494E-9ADD-72703EF32446
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6fe80c00537929b10bd7cd4d75d1bf2a5d065525
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581353"
---
# <a name="interrupts-from-spb-connected-peripheral-devices"></a>SPB 接続周辺機器からの割り込み


など、PCI バスとは異なり、[シンプルな周辺機器のバス](https://msdn.microsoft.com/library/windows/hardware/hh450903)(SPB) など、I²C または SPI、標準化、no を提供します。 バス固有意味周辺機器からすると、プロセッサの割り込み要求を伝達するためにします。 代わりに、SPB に接続された周辺機器は、SPB と SPB コントローラー両方の外側にある別のハードウェア パスを介して割り込みを通知します。 この割り込みパスの詳細は、次に 1 つのハードウェア プラットフォームによって異なる傾向がありますが、Windows は、さまざまなハードウェア プラットフォームで動作するドライバーを有効にする SPB に接続されている周辺機器デバイスのドライバーからこれらの詳細を非表示にします。




通常、SPB に接続されている周辺機器からの割り込み要求行が汎用入出力 (GPIO) コント ローラーで、暗証番号 (pin) に接続されているし、GPIO コント ローラーは、デバイスからすると、プロセッサの割り込みを中継します。 詳細については、[GPIO 割り込み](https://msdn.microsoft.com/library/windows/hardware/hh406467)を参照してください。

周辺機器のデバイス ドライバーは、抽象 Windows 割り込みリソースとしてこの GPIO 割り込みを取得 (**CmResourceTypeInterrupt**) し、ドライバーの割り込みサービス ルーチン (ISR) に割り込みを接続します。 割り込みリソースの抽象化では、ドライバーからの割り込みのプラットフォーム固有の詳細を非表示にします。 たとえば、ドライバーは、GPIO ピンから、または他のソースからの割り込みの受信かどうかなどの詳細情報を無視できます。 この抽象化を維持するために、DIRQL で実行され、カーネルの割り込みトラップ ハンドラーは、無音にアクティブな割り込み要求をクリアするか、一時的に GPIO ピンの割り込みをマスクする必要があります。 GPIO コント ローラーのハードウェア レジスタは、通常はメモリ マップし、DIRQL サービスにアクセスできます。

これに対し、SPB に接続されている周辺機器はメモリ マップしないと、このデバイスの ISR は IRQL で通常実行する必要があります = パッシブ\_レベル。 デバイスのハードウェア レジスタにアクセスするには、ISR は SPB 経由でシリアルの転送を実行する I/O 要求を送信します。 このような転送は、比較的低速 DIRQL で実行されている ISR では実行できません。 ただし、パッシブ レベル ISR は同期的に、I/O 要求を送信し、要求が完了するまでブロックします。

Edge によってトリガーされる、割り込みは、カーネルのトラップ ハンドラーは自動的に GPIO ピン、割り込み要求をクリアし、パッシブ レベルで実行するデバイスの ISR にスケジュールします。 トラップ ハンドラーを同じ割り込みがトラップ ハンドラーが戻った後でもう一度発生していることを防ぐために割り込みをオフにする必要があります。

レベル トリガーの割り込みのカーネルの割り込みのトラップ ハンドラーを自動的に GPIO ピン、割り込み要求を使用してパッシブ レベルで実行するデバイスの ISR にスケジュールします。 ISR は、デバイスからの割り込み要求をオフにする必要があります。 ISR を返した後、カーネルに GPIO ピンの割り込み要求に対してマスク解除します。

デバイスのパッシブ レベル ISR は、のみ、最初のサービス提供、割り込みを実行して、その他のデバイスのパッシブ レベル isr を特定の遅延を避けるを返す必要があります。 通常、ドライバーが ISR よりも低い優先順位で実行、割り込みワーカー スレッドに割り込みに関連する追加の処理を延期する必要があります。

Windows 8 では、以降では、[ユーザー モード ドライバー フレームワーク](https://msdn.microsoft.com/library/windows/hardware/ff560442)(UMDF) は、UMDF ドライバーの Isr をサポートしています。 SPB 周辺機器のデバイスの UMDF ドライバーは呼び出し、 [ **IWDFDevice3::CreateInterrupt** ](https://msdn.microsoft.com/library/windows/hardware/hh451208) ISR をデバイスからの割り込みに接続するメソッド。 デバイス信号を割り込み要求、カーネルのトラップ ハンドラーはパッシブ レベルで実行する ISR をスケジュールします。 詳細については、[へのアクセスのハードウェアと割り込み処理](https://msdn.microsoft.com/library/windows/hardware/hh439560)を参照してください。

Windows 8 では、以降では、[カーネル モード ドライバー フレームワーク](https://msdn.microsoft.com/library/windows/hardware/ff544296)(KMDF) は、パッシブ レベル Isr をサポートしています。 KMDF ドライバー SPB の周辺機器を呼び出し、 [ **WdfInterruptCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547345)割り込みにパッシブ レベル ISR をデバイスから接続するメソッド。 ポインターは、このメソッドへの入力パラメーターのいずれかを[ **WDF\_割り込み\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff552347)割り込みの構成情報を含む構造体。 パッシブのレベルで実行する ISR を構成する設定、 **PassiveHandling**をこの構造体のメンバー **TRUE**します。 詳細については、[パッシブ レベルの中断をサポートしている](https://msdn.microsoft.com/library/windows/hardware/hh451035)を参照してください。

 

 




