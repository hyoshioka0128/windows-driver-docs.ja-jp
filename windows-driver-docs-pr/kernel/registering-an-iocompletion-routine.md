---
title: IoCompletion ルーチンの登録
description: IoCompletion ルーチンの登録
ms.assetid: 413d8463-b2ce-44b6-846c-f853b5cd580e
keywords:
- IoCompletion ルーチン
- IoCompletion ルーチンを登録します。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: bca1045ab65bcb24097161d4b8efc3e6877d465c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571730"
---
# <a name="registering-an-iocompletion-routine"></a>IoCompletion ルーチンの登録





登録する、 [ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354) 、日常的なディスパッチ ルーチンを呼び出す[ **IoSetCompletionRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff549679)、を指定して*IoCompletion*ルーチンのアドレスとは、その後に渡されることを使用して下位のドライバーを IRP [**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)します。

呼び出し時に**IoSetCompletionRoutine**、ディスパッチ ルーチンが I/O マネージャーが呼び出すサーバーの指定した状況を指定します*IoCompletion*ルーチン。 選択できます、 *IoCompletion*下位レベルのドライバーが IRP を正常に完了する場合、ルーチンが呼び出されます (*InvokeOnSuccess*)、エラー状態の値を持つ IRP の完了 (*InvokeOnError*)、IRP をキャンセルするか (*InvokeOnCancel*)、任意の組み合わせ。

目的、 *IoCompletion*ルーチンは、下位レベルのドライバーが IRP にでしたを監視し、必要に応じて、追加の完了処理を実行します。 ドライバーの最も一般的なを使用して具体的には、 *IoCompletion*ルーチンが次に示します。

-   割り当てられて、ドライバーは IRP を破棄する[ **IoAllocateIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff548257)または[ **IoBuildAsynchronousFsdRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548310)

    高度なドライバーは IRP を使用してこれらのサポートのルーチンを指定する必要がありますのいずれかによって割り当てられる、 *IoCompletion*その IRP のルーチンです。 *IoCompletion*ルーチンを呼び出す必要があります[ **IoFreeIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff549113)ドライバーに割り当てられた Irp を破棄します。

-   要求元の要求を満足し、完了するまで、下位のドライバーがいくつかの部分の転送などの操作を完了する受信の IRP を再利用する、 *IoCompletion*ルーチン

-   下位のドライバーがエラーで完了した要求を再試行するには

    など、ファイル システムの最上位レベルのドライバーがある可能性が高い*IoCompletion*以上を除く、中間のドライバーを可能性がありますが、要求を再試行しようとするルーチン クラス ドライバーが密接に結合されたポート ドライバーの上に配置します。 ただし、ドライバーの使用を中間任意*IoCompletion*要求を再試行するルーチン。

最上位レベルまたは中間ドライバーの中に[ *DispatchReadWrite* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンは Irp を必要とするプロセスに最も可能性の高い、 *IoCompletion*ルーチン、ディスパッチIrp を下位のドライバーに渡される任意のドライバーのルーチンを登録できる、 *IoCompletion*ルーチン。

Irp のドライバーに割り当てられたと再利用の Irp では、ディスパッチ ルーチンを呼び出す必要があります**IoSetCompletionRoutine**次のブール型パラメーターを使用します。

-   *InvokeOnSuccess*設定**は TRUE。**

-   *InvokeOnError*設定**は TRUE。**

-   *InvokeOnCancel*設定**TRUE**場合は、チェーン内の下位のドライバーがキャンセル可能な Irp を処理

    通常、 *InvokeOnCancel*に設定されている**TRUE**IRP を状態と共に返される可能性があるかどうかに関係なく、\_取り消し済み、いることを確認する、 *IoCompletion*ルーチンは、各ドライバーに割り当てられた IRP の解放または IRP の各を再利用の完了ステータスを確認します。

使用してドライバを下の Irp を割り当てるディスパッチ ルーチン**IoAllocateIrp**または[ **IoBuildAsynchronousFsdRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548310)設定する必要があります、 *IoCompletion*各ドライバーに割り当てられた IRP のルーチンです。

-   ディスパッチ ルーチンは、IRP とその割り当てられた IRP(s) の元の両方についての状態を設定する必要があります、 *IoCompletion*ルーチンを使用します。 少なくとも、 *IoCompletion*ルーチンには、元の IRP へのアクセスが必要があり、割り当てられた数の追加 Irp の数。

-   ディスパッチ ルーチンを呼び出す必要があります**IoSetCompletionRoutine**すべて*InvokeOnXxx*のパラメーターを設定**TRUE**割り当てる IRP(s) の。

操作のシーケンスの Irp を再使用する、または I/O 操作を再試行するディスパッチ ルーチンを呼び出す必要があります**IoSetCompletionRoutine**再利用または再試行される各 IRP の。

-   ディスパッチ ルーチンを後で使用して、元の IRP の状態情報を保存する必要があります、 *IoCompletion*ルーチン。

    たとえば、 [ *DispatchReadWrite* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンが入力の IRP のパラメーターには、関連する転送の保存する必要があります、 *IoCompletion*部分をセットアップする前に日常的なその IRP で次の下位のドライバーを転送します。 パラメーターを保存することは特に重要だ場合、 *DispatchReadWrite*ルーチンは、任意のパラメーターを変更する、 *IoCompletion*ルーチンは、元の要求がされた時点を決定する必要があります満たされます。

-   場合、 *IoCompletion*ルーチンが、要求を再試行してください、ディスパッチ ルーチンは、再試行の回数のドライバーが指定の上限値を設定する必要があります、 *IoCompletion*ルーチンは、その前に試みる必要があります。エラーで元の IRP を完了します。

-   IRP が再利用する場合は、ディスパッチ ルーチンを呼び出す必要があります**IoSetCompletionRoutine**すべて*InvokeOnXxx*のパラメーターを設定**TRUE**します。

-   任意の中間ドライバーのディスパッチ ルーチンを呼び出す必要があります、非同期の要求の[ **IoMarkIrpPending** ](https://msdn.microsoft.com/library/windows/hardware/ff549422)元 IRP の。 状態を返す必要がありますし、その\_IRP が下位のドライバーに送信後に保留します。

 

 




