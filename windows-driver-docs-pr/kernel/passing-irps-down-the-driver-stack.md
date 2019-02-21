---
title: Irp がドライバー スタックを渡す
description: Irp がドライバー スタックを渡す
ms.assetid: 69d912c5-83cf-4651-b379-de6baea8ddd0
keywords:
- スタックを渡して、Irp WDK カーネル
- ドライバー スタック WDK ダウン Irp を渡す
- ドライバー スタック ダウン Irp を転送します。
- I/O スタックの場所の WDK カーネル
- スタックの場所の WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: bca7a2a342fae50c39b1d3e58fce128ce2fe8ea9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549225"
---
# <a name="passing-irps-down-the-driver-stack"></a>Irp がドライバー スタックを渡す





ドライバーのディスパッチ ルーチンは IRP を受信したときに呼び出す必要があります[ **IoGetCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff549174)ように独自 I/O スタックの場所を確認し、パラメーターが有効であるかを判断できます。 ドライバーが満たすことはできません自体、要求を完了する場合、次のいずれかをその。

-   さらに下位レベルのドライバーで処理するため IRP を渡します。

-   1 つまたは複数の新しい Irp を作成し、下位レベルのドライバーに渡したりします。

### <a name="a-higher-level-driver-should-pass-an-io-request-on-to-a-next-lower-driver-as-follows"></a>高度なドライバーは、次のように、I/O 要求を次の下位のドライバーを渡す必要があります。

1.  ディスパッチ ルーチンを呼び出す必要がある場合は、ドライバーは、[次へ] の下位レベルのドライバーには、入力 IRP を渡す、 [ **IoSkipCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff550355)または[ **IoCopyCurrentIrpStackLocationToNext** ](https://msdn.microsoft.com/library/windows/hardware/ff548387) I/O スタックの次の下位のドライバーの場所を設定します。

    ドライバーを呼び出す場合[ **IoAllocateIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff548257)追加 Irp の 1 つまたは複数の下位のドライバーを割り当てるにディスパッチ ルーチンは、次の手順に従って、次の下位ドライバーの I/O スタックの場所を初期化する必要があります記載されている[、中間レベルのドライバーでの処理の Irp](processing-irps-in-an-intermediate-level-driver.md)します。

    ディスパッチ ルーチンは、特定の要求に対して、次の下位ドライバーの I/O スタックの場所でのパラメーターの一部を変更できます。 たとえばより高度なドライバーは、基になるデバイスに既知の制限がある場合は、転送された容量では、大規模な転送要求のパラメーターを変更し、デバイス ドライバーの基になる部分転送要求を送信する IRP を再利用します。

2.  呼び出す[ **IoSetCompletionRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff549679)します。

    ディスパッチ ルーチンは、次の下位のドライバーに IRP を受信したを渡すことは、設定、 [ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)ルーチンは、省略可能ですが、便利なため、ルーチンが低い方法を決定するなどのタスクを実行できますドライバーは、部分的な転送の IRP を再利用、ドライバーは Irp を追跡する場合に、どのような状態の更新、およびエラーで返された要求を再試行は、要求を完了しました。

    ディスパッチ ルーチンには、新しい Irp が割り当て、設定、 *IoCompletion*ルーチンが必要なの下位のドライバーが完了した後に、ルーチンが各 IRP をリリースする必要があります。

    詳細については*IoCompletion*ルーチンを参照してください[Irp の完了](completing-irps.md)します。

3.  呼び出す[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)下位のドライバーによって処理される各 IRP にします。

4.  など、適切な NTSTATUS 値を返します。
    -   ステータス\_PENDING

        ドライバーが通常の状態を返します\_IRP の入力が、非同期の要求などに設定されている場合、保留[ **IRP\_MJ\_読み取り**](https://msdn.microsoft.com/library/windows/hardware/ff550794)または[ **IRP\_MJ\_書き込み**](https://msdn.microsoft.com/library/windows/hardware/ff550819)します。

    -   呼び出しの結果**保留**

        ドライバーが頻繁にへの呼び出しの結果を返します**保留**入力 IRP など、同期要求は、かどうか[ **IRP\_MJ\_作成**](https://msdn.microsoft.com/library/windows/hardware/ff550729).

### <a name="a-lowest-level-device-driver-passes-any-irp-that-it-cannot-complete-in-its-dispatch-routine-on-to-other-driver-routines-as-follows"></a>最下位レベルのデバイス ドライバーは次のように他のドライバーのルーチンへのディスパッチ ルーチンで完了できないことを任意の IRP に渡します。

1.  呼び出す[ **IoMarkIrpPending** ](https://msdn.microsoft.com/library/windows/hardware/ff549422) IRP の入力を使用します。

2.  呼び出す[ **IoStartPacket** ](https://msdn.microsoft.com/library/windows/hardware/ff550370)渡すか、キューの IRP がドライバーの[ *StartIo* ](https://msdn.microsoft.com/library/windows/hardware/ff563858)ドライバーは、独自の内部を管理しない限り、日常的なキュー、」の説明に従って IRP [Driver-Managed IRP キュー](driver-managed-irp-queues.md)します。

    ドライバーがない場合、 *StartIo*ルーチンですがキャンセル可能な Irp の処理、いずれかに登録する必要があります、 [*キャンセル*](https://msdn.microsoft.com/library/windows/hardware/ff540742)ルーチンまたは実装を[キャンセル セーフIRP キュー](cancel-safe-irp-queues.md)します。 詳細については*キャンセル*ルーチンを参照してください[キャンセル Irp](canceling-irps.md)します。

3.  状態を返す\_保留します。

 

 




