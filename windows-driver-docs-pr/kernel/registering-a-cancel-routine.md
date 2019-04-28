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
ms.openlocfilehash: f9b5316b713470832d64a5454e9c7f68309ed177
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382652"
---
# <a name="registering-a-cancel-routine"></a>キャンセル ルーチンの登録





デバイス ドライバーがある場合、 [ *StartIo* ](https://msdn.microsoft.com/library/windows/hardware/ff563858)そのディスパッチ ルーチンを登録できますで日常的な[*キャンセル*](https://msdn.microsoft.com/library/windows/hardware/ff540742)としてそのアドレスを指定して日常的な入力[ **IoStartPacket**](https://msdn.microsoft.com/library/windows/hardware/ff550370)します。

ドライバーがない場合、 *StartIo*日常的なそのディスパッチ ルーチンは IRP がキューの他のドライバーのルーチンでさらに処理する前に、次を行う必要があります。

1.  呼び出す[ **IoAcquireCancelSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff548196)します。

2.  呼び出す[ **IoSetCancelRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff549674)入力 IRP とドライバーが提供するためのエントリ ポイントを備えた*キャンセル*ルーチン。

3.  呼び出す[ **IoReleaseCancelSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff549550)します。

キャンセルのスピン ロックについては、次を参照してください。[システムのキャンセル スピン ロックを使用して](using-the-system-s-cancel-spin-lock.md)します。

I/O マネージャーが指定したデバイスのキューを使用するのではなく、Irp の独自のキューを管理するドライバーを呼び出すときに、キャンセル スピン ロックを取得する必要はありません**IoSetCancelRoutine**します。 ただし、これらのドライバーを確認する必要があります、*キャンセル*日常的なポインターを**IoSetCancelRoutine**判断を返すかどうか、*キャンセル*ルーチンが既に開始します。

 

 




