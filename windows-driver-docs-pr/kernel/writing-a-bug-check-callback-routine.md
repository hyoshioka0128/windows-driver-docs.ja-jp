---
title: バグ チェック コールバック ルーチンの記述
description: バグ チェック コールバック ルーチンの記述
ms.assetid: 62aefe67-e197-4c45-b994-19bd7369dbc1
keywords:
- バグ チェック コールバック ルーチン WDK カーネル
- コールバック ルーチン WDK のバグ チェック
- コールバック ルーチンを登録します。
- KeRegisterBugCheckCallback
- BugCheckCallback
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66ef9c90be5fe83827ead362cdc813fd95870fdc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327331"
---
# <a name="writing-a-bug-check-callback-routine"></a>バグ チェック コールバック ルーチンの記述





ドライバーは、システムのバグ チェックが発行するときに実行されるコールバック ルーチンを登録できます。

すべて NT ベースのオペレーティング システムでドライバーを使用できます、 [ **KeRegisterBugCheckCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff553105)を登録するルーチンを[ *BugCheckCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff540674)ルーチン、および[ **KeDeregisterBugCheckCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff551992)ルーチンを削除します。 ドライバーを使用できる、 *BugCheckCallback*ルーチンを自分のデバイスを既知の状態にリセットします。

Windows XP Service Pack 1 (SP1) および Windows Server 2003 では、前にドライバーを使用することも*BugCheckCallback*クラッシュ ダンプ ファイルにデータを格納する: システムでは、各と呼ばれる*BugCheckCallback*する前に日常的なクラッシュ ダンプ ファイルに渡されたバッファーに書き込まれるため、データを書き込む*BugCheckCallback*クラッシュ ダンプ ファイルに保存されていました。

Windows XP SP1 および Windows Server 2003 以降では、システムを呼び出す*BugCheckCallback*クラッシュ ダンプ ファイルが書き込まれるとします。 代わりに、システムでは、さらに 2 種類のバグ チェック コールバック ルーチンをサポートしています。 A [ *BugCheckSecondaryDumpDataCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff540679)クラッシュ ダンプ ファイルをセカンダリ データを書き込むルーチンを使用できます。 A [ *BugCheckDumpIoCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff540677)ルーチンを使用して、デバイスにクラッシュ ダンプ ファイルをコピーすることができます。

Windows Server 2008 および以降のバージョンの Windows でドライバーを実装できます、 [ *BugCheckAddPagesCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff540669)ルーチン クラッシュ ダンプ ファイルにドライバー固有のデータ ページを追加します。 異なり、 *BugCheckSecondaryDumpDataCallback*ルーチンで、セカンダリのクラッシュ ダンプのリージョンにデータを追加、 *BugCheckAddPagesCallback*ルーチンは、クラッシュ ダンプのリージョンにデータのページを追加します。 デバッグ中に、クラッシュ ダンプ データはセカンダリのクラッシュ ダンプ データよりも簡単にアクセスします。

ドライバーを使用して、 [ **KeRegisterBugCheckReasonCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff553110)と[ **KeDeregisterBugCheckReasonCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff552003)ルーチンを登録するにはこれら 3 種類の*BugCheckXxxCallback*コールバック ルーチン。

IRQL でバグ チェック コールバック ルーチンが実行される高 =\_レベルで、何ができるに厳密な制限が課されます。

バグ チェック コールバック ルーチンことはできません。

-   メモリの割り当て

-   ページング可能なメモリのアクセス

-   すべての同期機構を使用します。

-   IRQL で実行する必要がある任意のルーチンを呼び出すディスパッチ =\_レベル以下

バグ チェック コールバック ルーチンのため同期は必要ありません、中断せずに実行することが保証されます。 (バグ チェック ルーチンが任意の同期機構を使用している場合、システム デッドロックが発生します。)

ドライバーのバグ チェック コールバック ルーチンが安全に使用できます、<strong>読み取り\_ポート\_*XXX</strong><em>、*読み取り\_登録\_</em>XXX <strong><em>、*</em>書き込み\_ポート\_* XXX</strong><em>、および**書き込み\_登録\_</em>XXX*** ドライバーのデバイスと通信するルーチン。 (これらのルーチンの詳細については、次を参照してください[ハードウェア アブストラクション レイヤー ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff546644)。)。

バグ チェック コールバックの詳細については、次を参照してください[ *BugCheckCallback*](https://msdn.microsoft.com/library/windows/hardware/ff540674)、 [ *BugCheckAddPagesCallback*](https://msdn.microsoft.com/library/windows/hardware/ff540669)、 [ 。*BugCheckDumpIoCallback*](https://msdn.microsoft.com/library/windows/hardware/ff540677)、 [ *BugCheckSecondaryDumpDataCallback*](https://msdn.microsoft.com/library/windows/hardware/ff540679)、および[バグ チェック コールバック データの読み取り](https://msdn.microsoft.com/library/windows/hardware/ff553558).

 

 




