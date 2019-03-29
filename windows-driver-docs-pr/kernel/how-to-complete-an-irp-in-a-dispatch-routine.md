---
title: ディスパッチ ルーチン内で IRP を完了する方法
description: ディスパッチ ルーチン内で IRP を完了する方法
ms.assetid: b29da791-e768-4f67-8e85-6cfbeca97220
keywords:
- ルーチンをディスパッチ Irp WDK カーネルを完了すると、
- ディスパッチ ルーチンの WDK カーネル、Irp の完了
- WDK Irp のステータス情報
- I/O 状態ブロック WDK カーネル
- 状態ブロックの WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a6dbd1f49848deab86b69555a43806ea11459ce
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573993"
---
# <a name="how-to-complete-an-irp-in-a-dispatch-routine"></a>ディスパッチ ルーチン内で IRP を完了する方法





入力の IRP を直ちに完了する場合ディスパッチ ルーチンは、次を行います。

1.  セット、**状態**と**情報**IRP の I/O の状態のメンバーのブロックを適切な値は、一般に。

    -   ディスパッチの日常的なセット**状態**状態のいずれか\_成功または適切なエラーが発生する (ステータス\_*XXX*)、サポート ルーチンへの呼び出しによって返される値をとりますまたは、下位のドライバーによりの特定同期要求。

        下位レベルのドライバーが状態を返す場合\_保留中、高度なドライバーは呼び出す必要がありますいない[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343) IRP が、例外が 1 つの。高度なドライバーを同期させるイベントを使用してその[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)ルーチンと場合、ディスパッチ ルーチン、 *IoCompletion*日常的な信号イベントと状態を返します。\_詳細\_処理\_必要な作業です。 ディスパッチ ルーチンは、イベントを待機しを呼び出して**IoCompleteRequest** IRP を完了します。

    -   設定**情報**バイト数を正常に転送された読み取りなどのデータを転送または書き込み要求、要求が満たされた場合。

    -   設定**情報**状態で完了するその他の Irp の特定の要求に従って変化する値に\_成功します。

    -   設定**情報**によって異なりますが、警告状態が完了すると Irp の特定の要求の値に\_*XXX*します。 たとえば、設定は**情報**状態として、このような警告の転送されたバイト数に\_バッファー\_オーバーフローします。

    -   通常、その設定**情報**エラー状態で完了する要求をゼロに\_*XXX*します。

2.  呼び出し**IoCompleteRequest** IRP と*PriorityBoost* = IO\_いいえ\_インクリメントします。

3.  適切な状態を返します\_*XXX*状態の I/O ブロックで既に設定されています。 なおへの呼び出し**IoCompleteRequest**のため、既に完了した IRP の I/O 状態ブロックからディスパッチ ルーチンからの戻り値を設定することはできません、特定の IRP を呼び出し元がアクセスできなくなります。

**IRP を IoCompleteRequest を呼び出すためには、この実装ガイドラインに従います。**

常に呼び出す前に、ドライバーが保持している任意のスピン ロックを解放**IoCompleteRequest**します。

不確定な階層型ドライバーのチェーンでは特に、IRP の完了に時間がかかります。 高度なドライバーの場合、デッドロックが発生することがさらに、 *IoCompletion*ルーチンにスピン ロックが保持している下位のドライバーは IRP を送信します。

 

 




