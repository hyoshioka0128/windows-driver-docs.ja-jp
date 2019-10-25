---
title: キャンセルルーチンの実装
description: キャンセルルーチンの実装
ms.assetid: 243b623b-317c-4084-a753-940c91c4cc50
keywords:
- Irp の取り消し、ガイドライン
- キャンセルルーチン、ガイドライン
ms.date: 05/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 978f6aeef3c2f757bd8489eee5027290bfa695b2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838640"
---
# <a name="implementing-a-cancel-routine"></a>キャンセルルーチンの実装





I/o マネージャーは、入力 IRP が取り消され、i/o 要求のターゲットデバイスを表す*DeviceObject*ポインターを使用して、ドライバーが提供する[*キャンセル*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)ルーチンを呼び出します。

IRP は、現在の Win32 アプリケーションがユーザーによって閉じられているときと同じように、ドライバーの[*DispatchReadWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンがキューに入れられたものである可能性があります。 また、IRP は、基になるデバイスの性質に応じて、上位レベルのドライバーが明示的に取り消されたものである可能性もあります。

*キャンセル*ルーチンが呼び出されると、入力 IRP はターゲットデバイス**オブジェクトで既に存在して**いるか、またはドライバーに[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)ルーチンがある場合はターゲットデバイスオブジェクトに関連付けられているデバイスキューに既に存在している可能性があります。 ドライバーに*StartIo*ルーチンがない場合、irp は、*キャンセル*ルーチンが呼び出されたときに、ドライバーによって管理される irp の内部キューに存在する可能性があります。 どのような場合でも、i/o マネージャーは、受信した IRP の*キャンセル*ルーチンを呼び出す前に、この Irp の**Cancel**メンバーを**TRUE**に設定し、Irp の**cancelroutine**メンバーを**NULL**に設定します。

Irp が関連付けられているマスター IRP の*キャンセル*ルーチンは、 [**Iocancelirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocancelirp)を呼び出して、関連する irp をキャンセルします。

すべての*キャンセル*ルーチンは、次のガイドラインに従う必要があります。

-   [**IoReleaseCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549550(v=vs.85))を呼び出して、システムのキャンセルスピンロックを解除します。

-   I/o 状態ブロックの**状態**メンバーを [状態]\_[キャンセル] に設定し、その**情報**メンバーを0に設定します。

-   [**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出して、指定した IRP を完了します。

-   *キャンセル*ルーチンは常にシステムのキャンセルスピンロックを保持して呼び出されるため、このルーチンでは、最初に**IoReleaseCancelSpinLock**を呼び出さない限り、 [**IoAcquireCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548196(v=vs.85))を呼び出すことはできません。

-   *キャンセル*ルーチンは、コントロールを返すときにシステムキャンセルスピンロックを保持できません。 つまり、すべての*キャンセル*ルーチンは、制御を返す前に、少なくとも1回**IoReleaseCancelSpinLock**を呼び出す必要があります。

-   **IoAcquireCancelSpinLock**を呼び出す場合は、*キャンセル*ルーチンが**IoReleaseCancelSpinLock**への相互呼び出しをできるだけ早く行う必要があります。

-   スピンロックを保持しながら、IRP で[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出さないでください。 スピンロックを保持した状態で IRP を完了しようとすると、デッドロックが発生する可能性があります。


 

 




