---
title: パッシブ レベル割り込みサービス ルーチンの使用
description: Windows 8 以降、ドライバーはパッシブ レベル InterruptService ルーチン (ISR) を登録するのに IoConnectInterruptEx ルーチンを使用できます。
ms.assetid: 122BDE14-1552-4F7B-88D3-030423713E00
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8074e6ce4b083e1f94e857c1d2bdc0b1b217b123
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381582"
---
# <a name="using-passive-level-interrupt-service-routines"></a>パッシブ レベル割り込みサービス ルーチンの使用


Windows 8 以降、ドライバーを使用できます、 [ **IoConnectInterruptEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioconnectinterruptex)パッシブ レベルを登録するルーチン[ *InterruptService* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kservice_routine)ルーチン (ISR)。 関連付けられている割り込みが発生すると、カーネルの割り込みのトラップ ハンドラーは IRQL で実行するには、このルーチンをスケジュール設定 = パッシブ\_レベル。 ISR は、デバイスのハードウェア レジスタの I/O 要求を介してのみアクセスできる場合は、パッシブ レベルで実行する必要があります。 パッシブ レベル ISR synchrononously 送信 I/O デバイスへの要求し、要求が完了するまでブロックすることができます。

## <a name="registering-a-passive-level-isr"></a>パッシブ レベル ISR を登録します。


入力パラメーター **IoConnectInterruptEx**へのポインター、 [ **IO\_CONNECT\_INTERRUPT\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_connect_interrupt_parameters)構造体。 パッシブ レベル ISR を登録するには、設定、**バージョン**いずれかの接続にこの構造体のメンバー\_完全\_SPECIFIED または CONNECT\_行\_ベース。 場合**バージョン**= CONNECT\_完全\_、指定されたセット、 **Irql**パッシブにメンバー\_レベル、 **SynchronizeIrql**メンバーパッシブに\_レベル、および**スピンロック**メンバー **NULL**します。 場合**バージョン**= CONNECT\_行\_設定に応じて、 **SynchronizeIrql** = パッシブ\_レベルと**スピンロック** = **NULL**します。

割り込みオブジェクトが、パッシブ レベル ISR を指定する場合、 [ **KeSynchronizeExecution** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesynchronizeexecution)ルーチン スピン ロックではなく、の実行を同期するカーネル同期イベントオブジェクトを使用します。[*SynchCritSection* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-ksynchronize_routine) ISR ルーチン

このイベント オブジェクトに割り当てられる、 **IoConnectInterruptEx**パッシブ レベル ISR を登録する呼び出しで日常的な 呼び出し元は、この呼び出しでスピン ロックを指定しない必要があります。 (つまり、呼び出し元を設定する必要があります、**スピンロック**のメンバー、 **IO\_CONNECT\_割り込み\_パラメーター** ISR はパッシブ レベルで実行する場合は NULL に構造体します)。それ以外の場合、 **IoConnectInterruptEx**失敗し、エラーの状態を返します\_無効な\_パラメーター。

[ **KeAcquireInterruptSpinLock** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551914(v=vs.85))と[ **KeReleaseInterruptSpinLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleaseinterruptspinlock)ルーチン バグ チェックが発生する場合、指定の ISRIRQL で実行される割り込みオブジェクト = パッシブ\_レベル。

## <a name="devices-that-require-passive-level-interrupt-handling"></a>パッシブのレベルを必要とするデバイスの割り込み処理


レベルによってトリガーされる割り込み要求を通知する、メモリ マップト デバイス、デバイスの ISR 通常で呼び出されますから DIRQL、カーネルの割り込みのトラップ ハンドラー内で。 ISR では、割り込みをオフにするデバイスでのハードウェア レジスタを操作します。

ただし、ISR は IRQL で実行する必要があります = パッシブ\_レベルの場合は、関連するデバイスの通知レベルによってトリガーされる割り込み要求が、デバイスのハードウェアの登録は、カーネルの内から DIRQL で呼び出される ISR から直接アクセスできません割り込みトラップ ハンドラー。 たとえば、デバイスのレジスタが可能性がありますメモリ マップトにできないか、ISR がレジスタへのアクセス中に一時的にブロックされる可能性があります。

Windows 8 以降、ドライバーはパッシブ レベル ISR. を登録できます。 割り込みが発生すると、カーネルの割り込みのトラップ ハンドラーは IRQL で実行する ISR をスケジュール設定 = パッシブ\_レベル。 割り込みコント ローラーに割り込みをミュートする必要があります、ハンドラーから制御が戻る前に (または[GPIO コント ローラー](https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-driver-support-overview))。 デバイス信号を edge によってトリガーされる割り込み、ハンドラーは、割り込みコント ローラーに割り込みをクリアします。 デバイス信号レベルによってトリガーされる割り込みを場合、ハンドラーが割り込みコント ローラーに割り込みを一時的にマスクします。ISR を実行した後、カーネルには、割り込みに対してマスク解除します。

## <a name="an-example"></a>例


パッシブ レベル ISR が必要となるデバイスの例は、I²C などの低電力シリアル バスに接続されているセンサー デバイスです。 I²C およびその他のサポート Windows 8 以降、[単純な周辺機器のバス](https://docs.microsoft.com/previous-versions/hh450903(v=vs.85))(SPBs) によって提供される、 [SPB フレームワーク拡張](https://docs.microsoft.com/windows-hardware/drivers/spb/spb-framework-extension)(SpbCx)。

I²C に接続されたセンサー デバイスの登録にアクセスするには、センサー ドライバーは、I/O 要求とコント ローラーのドライバー、バスを SpbCx によって共同で処理するセンサー デバイスを送信します。 要求された操作を実行するには、SPB コント ローラーする必要がありますデータ転送逐次的に、バス経由で。 この転送は、比較的低速 DIRQL で実行されている ISR の時間の制約内で実行することはできません。 ただし、パッシブ レベル ISR は同期的に I/O 要求を送信し、要求が完了するまでブロックします。

この例ではパッシブ レベル ISR は、ISR が中断する必要のデバイスを I/O 要求を送信すると、I²C バス コント ローラーがオフの場合、時間が長くなるのブロックがあります。 この場合、コント ローラーは、バス経由でデータを転送に前に、D0 電源の状態への移行を完了する必要があります。

PCI などのバスとは異なり、I²C bus は、この例では、周辺機器からすると、プロセッサの割り込み要求を伝達するためには意味 bus 固有を提供します。 代わりに、センサー デバイスは、割り込みをプロセッサの割り込み要求をリレーし、GPIO コント ローラーのデバイスで pin を通知する場合があります。 詳細については、次を参照してください。 [GPIO 割り込み](https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-interrupts)します。

通常、GPIO コント ローラーのハードウェア レジスタはメモリ マップし、カーネルの割り込みのトラップ ハンドラーで DIRQL サービスにアクセスできます。 センサー デバイスでは、割り込みが発生するときに、ハンドラーは GPIO コント ローラーのレジスタに割り込みビットを操作することによって、割り込みを無音する必要があります。

レベル トリガーの割り込みのカーネルの割り込みのトラップ ハンドラーを GPIO ピン、割り込み要求を使用してし、センサー デバイスの ISR パッシブ レベルで実行するスケジュールを設定します。 ISR は、センサー デバイスからの割り込み要求をオフにする必要があります。 ISR を返した後、カーネルに GPIO ピンの割り込み要求に対してマスク解除します。

Edge によってトリガーされる、割り込みは、カーネルのトラップ ハンドラーは、GPIO ピン、割り込み要求をクリアし、センサー デバイスの ISR パッシブ レベルで実行するスケジュールを設定します。

## <a name="worker-routines"></a>ワーカーのルーチン


呼び出しで**IoConnectInterruptEx**ドライバーがパッシブ レベル ISR とワーカーのルーチンの割り込みの処理に分割するオプション。 一般的な規則として ISR は割り込み (たとえば、無音レベルによってトリガーされる割り込み) の初期処理を実行し、作業者に追加の処理を延期する必要があります。 ISR とワーカーの両方は、パッシブ レベルで実行してが ISR は相対的に高い優先順位で実行され、他の優先度の高いタスクに遅れる可能性があります。 これらのタスクは、新しい割り込みのパッシブ レベル Isr を含めることができます。

まれなケースでは、割り込み処理パッシブ レベル ISR は、割り込みのすべての処理を実行できるし、ワーカーのルーチンは必要ないことはあまり必要があります。

KMDF ドライバーでパッシブ レベル isr を特定の使用方法の詳細については、次を参照してください。[パッシブ レベルの中断をサポートしている](https://docs.microsoft.com/windows-hardware/drivers/wdf/supporting-passive-level-interrupts)します。

 

 




