---
title: ディスパッチルーチンで IRP を完了する方法
description: ディスパッチルーチンで IRP を完了する方法
ms.assetid: b29da791-e768-4f67-8e85-6cfbeca97220
keywords:
- Irp WDK カーネル、ディスパッチルーチンを完了する
- ディスパッチルーチン WDK カーネル、Irp の完了
- ステータス情報 WDK Irp
- I/o ステータスが WDK カーネルをブロックする
- 状態は WDK カーネルをブロックします
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1176863800cb93ab75e1634d2052fb6ca46cd592
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838643"
---
# <a name="how-to-complete-an-irp-in-a-dispatch-routine"></a>ディスパッチルーチンで IRP を完了する方法





入力 IRP をすぐに完了できる場合、ディスパッチルーチンは次の処理を実行します。

1.  IRP の i/o 状態ブロックの**状態**と**情報**メンバーを適切な値に設定します。通常は次のとおりです。

    -   ディスパッチルーチンは、**状態\_** を [成功] または適切なエラー (ステータス\_*XXX*) に設定します。これは、サポートルーチンへの呼び出しによって返される値、または特定の同期要求に対して下位のドライバーによって返される値になります。

        下位レベルのドライバーから状態\_が返された場合、上位レベルのドライバーは、IRP の[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出すことはできません。ただし、上位レベルのドライバーは、イベントを使用して、 [*iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンとの間で同期を行うことができます。ディスパッチルーチン。この場合、 *Iocompletion*ルーチンはイベントを通知し、必要な\_処理\_より多くのステータス\_を返します。 ディスパッチルーチンは、イベントを待機してから、 **IoCompleteRequest**を呼び出して IRP を完了します。

    -   読み取りまたは書き込み要求などのデータ転送要求が満たされた場合に、正常に転送されたバイト数に**情報**を設定します。

    -   この例では、状態\_SUCCESS で完了した他の Irp の特定の要求に応じて変化する値に**情報**を設定します。

    -   **情報**は、警告ステータス\_*XXX*で完了した irp の特定の要求に応じて変化する値に設定されます。 たとえば、状態\_バッファー\_オーバーフローなどの警告に対して転送されたバイト数**を設定し**ます。

    -   通常は、エラー状態\_*XXX*で、完了した要求に対して**情報**を0に設定します。

2.  は、IoCompleteRequest を使用して、IRP を使用してを呼び出します。優先度*ブースト*= IO\_\_インクリメントはありません。

3.  は、i/o 状態ブロックに既に設定されている適切な状態\_*XXX*を返します。 **IoCompleteRequest**を呼び出すと、指定された irp が呼び出し元によってアクセス不可能になるため、ディスパッチルーチンからの戻り値を、既に完了した irp の i/o 状態ブロックから設定することはできません。

**IRP で IoCompleteRequest を呼び出すには、次の実装ガイドラインに従います。**

**IoCompleteRequest**を呼び出す前に、ドライバーが保持しているスピンロックを常に解放します。

特に、階層化されたドライバーのチェーンでは、IRP の完了には不確定の時間がかかります。 さらに、上位レベルのドライバーの*Iocompletion*ルーチンが、スピンロックを保持している下位のドライバーに IRP を戻すと、デッドロックが発生する可能性があります。

 

 




