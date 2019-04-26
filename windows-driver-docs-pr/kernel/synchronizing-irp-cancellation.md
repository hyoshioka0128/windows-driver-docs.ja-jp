---
title: IRP キャンセルの同期
description: IRP キャンセルの同期
ms.assetid: a110c6ad-794d-4b8a-a89d-bceb08ea82b8
keywords:
- Irp、同期をキャンセル
- キャンセル ルーチンでは、同期
- WDK Irp の同期
- Irp WDK のキャンセル可能なカーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c25b2fd53bf4b3079839853dac31f6475d17279b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345433"
---
# <a name="synchronizing-irp-cancellation"></a>IRP キャンセルの同期





ドライバーの観点からは IRP をいつでもキャンセルできます。 IRP のキャンセルに非同期的に発生しますそのため、ドライバーは、多数の潜在的な競合状態、IRP が、次の点のいずれかで取り消された場合の作成を処理できる必要があります。

-   ドライバーのルーチンが呼び出された後が IRP をキューに配置する前に。

-   ルーチンは、ドライバーの後に呼び出されるしますが、IRP の処理を試みる前にします。 たとえば、ドライバーの後に IRP をキャンセルする可能性があります[ *StartIo* ](https://msdn.microsoft.com/library/windows/hardware/ff563858)ルーチンを呼び出すと、前に、 *StartIo*ルーチン IRP をデバイスのキューから削除します。

-   ルーチンはドライバーの後に、IRP をデキューが要求された I/O を開始する前にします。

ドライバーは IRP のキューしキューを保護するスピン ロックは解放、別のスレッドにアクセスして IRP の変更に注意してください。 元のスレッドを再開したとき-もすぐに次のコード行: IRP を既にされた可能性がありますがキャンセルまたはそれ以外の場合は変更します。

ドライバーでは、IRP のキューを実装するために、キャンセルの安全な IRP のキューのフレームワークを使用できます。 システムを登録し、 [*キャンセル*](https://msdn.microsoft.com/library/windows/hardware/ff540742) Irp をキャンセルしても安全に同期を自動的に処理するドライバーの日常的な。 参照してください[キャンセル セーフ IRP キュー](cancel-safe-irp-queues.md)詳細についてはします。 それ以外の場合、ドライバーは、独自の同期を実装する必要があります。

IRP の次のメンバーには、取り消し処理についての情報が含まれます。

-   **Irp -&gt;キャンセル**IRP が取り消されているか、取り消す必要があるかどうかを示します。

-   **Irp -&gt;CancelRoutine** IRP がキャンセル可能かどうかを示します。 このメンバーにキャンセル ルーチンへのポインターが含まれている場合、IRP がキャンセル可能です。 このメンバーがある場合**NULL**IRP は取り消し可能ではありません。 このメンバーがある場合**NULL**が**Irp -&gt;キャンセル**がキャンセル ルーチンが実行されていると、IRP が取り消されていることを示す設定。

ドライバーは、キャンセル可能な Irp を処理する場合は、設定、適切な責任を負います*キャンセル*取り消しできる状態で保持している各の IRP で日常的な。

このセクションには、IRP のキャンセルを同期する方法は、次のトピックが含まれています。

[システムのキャンセル スピン ロックを使用します。](using-the-system-s-cancel-spin-lock.md)

[Irp を処理するルーチンをドライバーでの同期のキャンセル](synchronizing-cancellation-in-driver-routines-that-process-irps.md)

[キャンセル ルーチンなしの上位レベルのドライバーでの取り消し処理の同期](synchronizing-cancellation-in-higher-level-drivers-without-cancel-rout.md)

[ドライバーによって提供されるスピン ロックを使用します。](using-a-driver-supplied-spin-lock.md)

 

 




