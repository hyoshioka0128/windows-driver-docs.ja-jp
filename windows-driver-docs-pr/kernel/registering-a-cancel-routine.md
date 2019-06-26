---
title: キャンセル ルーチンの登録
description: キャンセル ルーチンの登録
ms.assetid: ebc63fb6-bf4d-4de3-9232-08d810c2f730
keywords:
- キャンセル ルーチンを登録する Irp のキャンセル
- キャンセル ルーチンを登録します。
- キャンセル ルーチンを登録します。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c514e4e81df7ff4c29b2bbbe10961f3fd8343e6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378730"
---
# <a name="registering-a-cancel-routine"></a>キャンセル ルーチンの登録





デバイス ドライバーがある場合、 [ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)そのディスパッチ ルーチンを登録できますで日常的な[*キャンセル*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_cancel)としてそのアドレスを指定して日常的な入力[ **IoStartPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostartpacket)します。

ドライバーがない場合、 *StartIo*日常的なそのディスパッチ ルーチンは IRP がキューの他のドライバーのルーチンでさらに処理する前に、次を行う必要があります。

1.  呼び出す[ **IoAcquireCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548196(v=vs.85))します。

2.  呼び出す[ **IoSetCancelRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcancelroutine)入力 IRP とドライバーが提供するためのエントリ ポイントを備えた*キャンセル*ルーチン。

3.  呼び出す[ **IoReleaseCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549550(v=vs.85))します。

キャンセルのスピン ロックについては、次を参照してください。[システムのキャンセル スピン ロックを使用して](using-the-system-s-cancel-spin-lock.md)します。

I/O マネージャーが指定したデバイスのキューを使用するのではなく、Irp の独自のキューを管理するドライバーを呼び出すときに、キャンセル スピン ロックを取得する必要はありません**IoSetCancelRoutine**します。 ただし、これらのドライバーを確認する必要があります、*キャンセル*日常的なポインターを**IoSetCancelRoutine**判断を返すかどうか、*キャンセル*ルーチンが既に開始します。

 

 




