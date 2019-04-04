---
title: 上位レベルのドライバーで DispatchReadWrite
description: 上位レベルのドライバーで DispatchReadWrite
ms.assetid: d8406115-c62e-4362-8d2c-77d0414c4104
keywords:
- DispatchReadWrite ルーチン
- ディスパッチ ルーチンの WDK カーネル、DispatchReadWrite ルーチン
- 読み取り/書き込みディスパッチ ルーチン WDK カーネル
- IRP_MJ_WRITE I/O 関数のコード
- IRP_MJ_READ I/O 関数のコード
- データ転送の WDK カーネル、読み取り/書き込みディスパッチ ルーチン
- データ転送の WDK カーネル、読み取り/書き込みディスパッチ ルーチン
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9437729bd477f3489265614a6b35d502065600b2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548803"
---
# <a name="dispatchreadwrite-in-higher-level-drivers"></a>上位レベルのドライバーで DispatchReadWrite





ファイル システム ドライバーを除くより高度なドライバーは、通常はありませんすべてのドライバーの内部キュー Irp の。 このようなドライバーの[ *DispatchReadWrite* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン渡すことができます Irp 下位のドライバーに有効なパラメーターを持つ可能性がありますを設定した後、 [ *IoCompletion*](https://msdn.microsoft.com/library/windows/hardware/ff548354) 」の説明に従って、ルーチン[ドライバー スタックを渡して Irp](passing-irps-down-the-driver-stack.md)します。

ただし、SCSI クラス ドライバーの*DispatchReadWrite*ルーチンは IRP を主な機能のコードを送信する前に、必要に応じて、大規模な転送要求を分割[ **IRP\_MJ\_読み取り**](https://msdn.microsoft.com/library/windows/hardware/ff550794)または[ **IRP\_MJ\_書き込み**](https://msdn.microsoft.com/library/windows/hardware/ff550819) SCSI ポート/ミニポート ドライバーのペアにします。 詳細については、[記憶域クラス ドライバー SplitTransferRequest ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff566965)を参照してください。

高度なドライバーがセットアップで次の下位のドライバーを 1 つまたは複数の Irp を割り当てた場合、 *DispatchReadWrite*ルーチンは、いくつかの部分の転送を要求する、 *DispatchReadWrite*ルーチンを呼び出す必要があります[ **IoSetCompletionRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff549679)各ドライバーに割り当てられた IRP にします。 ドライバーを登録する必要があります、 *IoCompletion*ルーチンを各部分転送操作で転送されるデータの量を追跡するように、 *IoCompletion*ルーチンは、すべてのドライバーに割り当てられた Irp をリリースできますと、最終的には、元の要求を完了します。

基になるドライバーでは、リムーバブル メディア デバイスを制御する上位レベルのドライバーによって割り当てられた任意の Irp にスレッド コンテキストが必要です。 スレッド コンテキストを設定する割り当てのドライバーが設定する必要があります、 **Irp -&gt;Tail.Overlay**します。各スレッドは IRP の着信の転送に同じ値から IRP を新しく割り当てられます。 詳細については、[リムーバブル メディアをサポートしている](supporting-removable-media.md)を参照してください。

部分の転送エラーが基になるデバイス ドライバーが IRP を返す場合、 *IoCompletion*ルーチンできます部分転送要求を再試行または I/O 状態ブロックは、返された設定の元の IRP の完了任意の Irp とより高度なドライバーのメモリを解放することが割り当てられた後は、エラーです。

より高度なドライバーの場合、 *DispatchReadWrite*ルーチンは、部分的な転送操作のメモリを割り当て、その割り当ては、ドライバーのによってアクセスされる*IoCompletion*ルーチン (または、基になるデバイス ドライバー)、 *DispatchReadWrite*ルーチンが非ページ プールからそのメモリを割り当てる必要があります。

 

 




