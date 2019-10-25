---
title: IRP キャンセルの同期
description: IRP キャンセルの同期
ms.assetid: a110c6ad-794d-4b8a-a89d-bceb08ea82b8
keywords:
- Irp の取り消し、同期
- キャンセルルーチン、同期
- WDK Irp の同期
- 取り消し可能 Irp WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e6780fe0356e005b2baaa25c6aebed83d2a4112c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836163"
---
# <a name="synchronizing-irp-cancellation"></a>IRP キャンセルの同期





ドライバーの観点からは、IRP はいつでも取り消すことができます。 IRP のキャンセルが非同期に行われます。したがって、次のいずれかの時点で IRP が取り消された場合に作成される、潜在的な競合状態の多くをドライバーが処理できる必要があります。

-   ドライバールーチンが呼び出された後、が IRP をキューに置いた後。

-   ドライバールーチンが呼び出された後、IRP の処理を試みる前。 たとえば、IRP は、ドライバーの[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)ルーチンが呼び出された後、 *StartIo*ルーチンがデバイスキューから irp を削除する前にキャンセルされる場合があります。

-   ドライバールーチンが IRP をデキューした後、要求された i/o を開始する前。

ドライバーが IRP をキューに置いて、キューを保護するすべてのスピンロックを解放すると、別のスレッドが IRP にアクセスして変更できることに注意してください。 元のスレッドが再開されたとき (次のコード行の直後でも)、IRP は既に取り消されているか、または変更されている可能性があります。

ドライバーは、キャンセルセーフな IRP キューフレームワークを使用して、IRP キューを実装できます。 次に、Irp を安全にキャンセルするために同期を自動的に処理するドライバーの[*キャンセル*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)ルーチンが登録されます。 詳細については[、「キャンセルセーフな IRP キュー](cancel-safe-irp-queues.md) 」を参照してください。 それ以外の場合、ドライバーは独自の同期を実装する必要があります。

IRP の次のメンバーには、キャンセルに関する情報が含まれています。

-   **Irp&gt;Cancel**は、irp が取り消されているか、取り消す必要があるかどうかを示します。

-   **Irp&gt;CancelRoutine**は、irp がキャンセル可能かどうかを示します。 このメンバーにキャンセルルーチンへのポインターが含まれている場合、IRP はキャンセル可能です。 このメンバーが**NULL**の場合、IRP はキャンセルできません。 このメンバーが**NULL**でも、 **irp&gt;cancel**が設定されている場合は、キャンセルルーチンが実行中で、irp がキャンセル処理中であることを示します。

ドライバーがキャンセル可能な Irp を処理する場合は、キャンセル可能な状態で保持されている各 IRP で適切な*キャンセル*ルーチンを設定する必要があります。

ここでは、IRP のキャンセルの同期に関する次のトピックについて説明します。

[システムのキャンセルスピンロックの使用](using-the-system-s-cancel-spin-lock.md)

[Irp を処理するドライバールーチンでのキャンセルの同期](synchronizing-cancellation-in-driver-routines-that-process-irps.md)

[キャンセルルーチンを使用しない、上位レベルのドライバーでのキャンセルの同期](synchronizing-cancellation-in-higher-level-drivers-without-cancel-rout.md)

[ドライバーによって提供されるスピンロックの使用](using-a-driver-supplied-spin-lock.md)

 

 




