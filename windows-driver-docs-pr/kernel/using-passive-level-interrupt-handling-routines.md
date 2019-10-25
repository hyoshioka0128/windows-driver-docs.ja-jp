---
title: パッシブ レベル割り込みサービス ルーチンの使用
description: Windows 8 以降では、ドライバーは IoConnectInterruptEx ルーチンを使用して、パッシブレベルの InterruptService ルーチン (ISR) を登録できます。
ms.assetid: 122BDE14-1552-4F7B-88D3-030423713E00
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 95eeabc811ae2eab45d6e57cdaa62af37b73303b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835919"
---
# <a name="using-passive-level-interrupt-service-routines"></a>パッシブ レベル割り込みサービス ルーチンの使用


Windows 8 以降では、ドライバーは[**IoConnectInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterruptex)ルーチンを使用して、パッシブレベルの[*INTERRUPTSERVICE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kservice_routine)ルーチン (ISR) を登録できます。 関連付けられている割り込みが発生すると、カーネルの割り込みトラップハンドラーによって、このルーチンが IRQL = パッシブ\_レベルで実行されるようにスケジュールされます。 I/o 要求によってのみデバイスのハードウェアレジスタにアクセスできる場合、ISR はパッシブレベルで実行する必要があります。 パッシブレベルの ISR は、synchrononously がデバイスに i/o 要求を送信し、要求が完了するまでブロックすることができます。

## <a name="registering-a-passive-level-isr"></a>パッシブレベルの ISR の登録


**IoConnectInterruptEx**への入力パラメーターは、 [**IO\_CONNECT\_INTERRUPT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_connect_interrupt_parameters)構造体へのポインターです。 パッシブレベルの ISR を登録するには、この構造体の**バージョン**メンバーを、\_完全に指定された\_接続するか、\_の行\_ベースとして接続するように設定します。 **Version** = CONNECT\_完全に\_指定されている場合は、 **IRQL**メンバーをパッシブ\_レベル、 **SYNCHRONIZEIRQL**メンバーをパッシブ\_レベル、**スピンロック**メンバーを**NULL**に設定します。 **Version** = CONNECT\_LINE\_BASED の場合は、set **SynchronizeIrql** = パッシブ\_LEVEL と**スピン = ロック**を**NULL**に設定します。

Interrupt オブジェクトがパッシブレベルの ISR を指定する場合、 [**KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)ルーチンは、 [*SynchCritSection*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine)ルーチンの実行を ISR と同期するために、スピンロックではなくカーネル同期イベントオブジェクトを使用します。

このイベントオブジェクトは、パッシブレベルの ISR を登録する呼び出しの**IoConnectInterruptEx**ルーチンによって割り当てられます。 呼び出し元は、この呼び出しにスピンロックを指定することはできません。 (つまり、ISR がパッシブレベルで実行される場合、呼び出し元は、 **IO\_接続\_割り込み\_パラメーター**構造体の**スピンロック**メンバーを NULL に設定する必要があります)。それ以外の場合、 **IoConnectInterruptEx**は失敗し、エラー状態の状態\_無効な\_パラメーターとして返されます。

[**KeAcquireInterruptSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551914(v=vs.85))ルーチンと[**KeReleaseInterruptSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinterruptspinlock)ルーチンは、指定された interrupt オブジェクトの ISR が IRQL = パッシブ\_レベルで実行されているかどうか、バグチェックを発生させます。

## <a name="devices-that-require-passive-level-interrupt-handling"></a>パッシブレベルの割り込み処理を必要とするデバイス


レベルでトリガーされる割り込み要求を通知するメモリマップトデバイスの場合、通常、デバイスの ISR はカーネルの割り込みトラップハンドラー内から DIRQL で呼び出されます。 ISR は、デバイス内のハードウェアレジスタを操作して割り込みをオフにします。

ただし、関連付けられているデバイスがレベルでトリガーされる割り込み要求を通知しても、デバイスのハードウェアレジスタがカーネル内から DIRQL で呼び出された ISR から直接アクセスできない場合、ISR は IRQL = パッシブ\_レベルで実行する必要があります。割り込みトラップハンドラー。 たとえば、デバイスレジスタがメモリにマップされていない場合や、レジスタアクセス中に ISR が一時的にブロックされる場合があります。

Windows 8 以降では、ドライバーはパッシブレベルの ISR を登録できます。 割り込みが発生すると、カーネルの割り込みトラップハンドラーは、IRQL = パッシブ\_レベルで実行するように ISR をスケジュールします。 ハンドラーが戻る前に、割り込みコントローラー (または[GPIO コントローラー](https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-driver-support-overview)) の割り込みを無音にする必要があります。 デバイスがエッジによってトリガーされる割り込みを通知する場合、ハンドラーは割り込みコントローラーの割り込みをクリアします。 デバイスがレベルでトリガーされた割り込みを通知する場合、ハンドラーは一時的に割り込みコントローラーの割り込みをマスクします。ISR の実行後、カーネルは割り込みをマスク解除します。

## <a name="an-example"></a>例


パッシブレベルの ISR を必要とするデバイスの例として、低電力のシリアルバスに接続されているセンサーデバイス (I ² C など) があります。 Windows 8 以降では、I ² C とその他の[単純な周辺機器](https://docs.microsoft.com/previous-versions/hh450903(v=vs.85))(spbs) のサポートは、 [SPB framework extension](https://docs.microsoft.com/windows-hardware/drivers/spb/spb-framework-extension) (spbcx) によって提供されています。

I ² C に接続されたセンサーデバイスのレジスタにアクセスするために、センサードライバーは、センサーデバイスに i/o 要求を送信します。この要求は、SpbCx とバスのコントローラードライバーによって共同で処理されます。 要求された操作を実行するには、SPB コントローラーがバス上でデータを直列に転送する必要があります。 この転送は比較的低速であり、DIRQL で実行される ISR の時間制約内で実行することはできません。 ただし、パッシブレベルの ISR は i/o 要求を同期的に送信し、要求が完了するまでブロックすることができます。

この例のパッシブレベルの ISR は、ISR が i/o 要求を中断中のデバイスに送信するときに、I ² C バスコントローラーがオフになっている場合に、長時間ブロックされる可能性があります。 この場合、コントローラーは、データをバス上に転送する前に、D0 電源状態への遷移を完了する必要があります。

PCI などのバスとは対照的に、この例の I ² C バスは、周辺機器からプロセッサに割り込み要求を伝えるためのバス固有の手段を提供しません。 代わりに、センサーデバイスが GPIO コントローラーデバイスの pin に割り込みを通知し、割り込み要求がプロセッサにリレーされることがあります。 詳細については、「 [GPIO 割り込み](https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-interrupts)」を参照してください。

通常、GPIO コントローラーのハードウェアレジスタはメモリにマップされ、カーネルの割り込みトラップハンドラーによって DIRQL でアクセスできます。 センサーデバイスで割り込みが発生した場合、ハンドラーは、GPIO コントローラーのレジスタの割り込みビットを操作することによって、割り込みを無音にする必要があります。

レベルでトリガーされる割り込みの場合、カーネルの割り込みトラップハンドラーによって、GPIO ピンで割り込み要求がマスクされ、センサーデバイスの ISR がパッシブレベルで実行されるようにスケジュールされます。 ISR は、センサーデバイスからの割り込み要求をクリアする必要があります。 ISR から制御が戻った後、カーネルは、GPIO ピンで割り込み要求をマスク解除します。

エッジによってトリガーされる割り込みの場合、カーネルのトラップハンドラーによって、GPIO ピンで割り込み要求がクリアされ、センサーデバイスの ISR がパッシブレベルで実行されるようにスケジュールされます。

## <a name="worker-routines"></a>ワーカールーチン


**IoConnectInterruptEx**の呼び出しでは、ドライバーは、パッシブレベルの ISR とワーカールーチン間の割り込み処理を分割するオプションを備えています。 一般的なルールとして、ISR は割り込みの初期処理を実行し (たとえば、レベルでトリガーされる割り込みを無音にする)、ワーカーへの追加処理を遅延させる必要があります。 ISR と worker はどちらもパッシブレベルで実行されますが、ISR は相対的に高い優先順位で実行され、他の優先度の高いタスクが遅れる可能性があります。 これらのタスクには、新しい割り込みのパッシブレベルの Isr が含まれる場合があります。

まれに、割り込みによって、パッシブレベルの ISR が割り込みの処理をすべて実行できるようにする必要があるため、ワーカールーチンは不要です。

KMDF ドライバーでのパッシブレベルの Isr の使用の詳細については、「[パッシブレベルの割り込みのサポート](https://docs.microsoft.com/windows-hardware/drivers/wdf/supporting-passive-level-interrupts)」を参照してください。

 

 




