---
title: キャンセル ルーチンの登録
description: キャンセル ルーチンの登録
ms.assetid: ebc63fb6-bf4d-4de3-9232-08d810c2f730
keywords:
- Irp の取り消し、キャンセルルーチンの登録
- キャンセルルーチン、登録
- キャンセルルーチンを登録しています
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc0d922f4beca83746545e8084075667d499a39e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827578"
---
# <a name="registering-a-cancel-routine"></a>キャンセル ルーチンの登録





デバイスドライバーに[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)ルーチンが含まれている場合、そのディスパッチルーチンは、そのアドレスを[**iostartpacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartpacket)への入力として指定することによって、[*キャンセル*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)ルーチンを登録できます。

ドライバーに*StartIo*ルーチンがない場合、そのディスパッチルーチンは、IRP をキューに追加して他のドライバールーチンによる後続の処理を実行する前に、次の操作を行う必要があります。

1.  [**IoAcquireCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548196(v=vs.85))を呼び出します。

2.  入力 IRP とドライバーが提供する*キャンセル*ルーチンのエントリポイントを使用して、 [**Iosetcancelroutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcancelroutine)を呼び出します。

3.  [**IoReleaseCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549550(v=vs.85))を呼び出します。

[キャンセル] スピンロックの詳細については、「[システムのキャンセルスピンロックの使用](using-the-system-s-cancel-spin-lock.md)」を参照してください。

I/o マネージャーが提供するデバイスキューを使用するのではなく、独自の Irp のキューを管理するドライバーは、 **Iosetcancelroutine**を呼び出すときに、キャンセルスピンロックを取得する必要はありません。 ただし、これらのドライバーは、 **Iosetcancelroutine**が返す*キャンセル*ルーチンポインターを確認して、*キャンセル*ルーチンが既に開始されているかどうかを確認する必要があります。

 

 




