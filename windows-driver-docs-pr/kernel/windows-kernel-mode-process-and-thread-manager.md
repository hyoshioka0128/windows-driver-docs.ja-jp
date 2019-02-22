---
title: Windows カーネル モード プロセスとスレッド マネージャー
description: Windows カーネル モード プロセスとスレッド マネージャー
ms.assetid: 4053c73e-190d-4ffe-8db2-f531d120ba81
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7eb171169fa476b5c0c74a53f3e9ff7c6d2695f1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539453"
---
# <a name="windows-kernel-mode-process-and-thread-manager"></a>Windows カーネル モード プロセスとスレッド マネージャー


A*プロセス*は Windows で現在実行中のソフトウェア プログラムです。 各プロセスには、ID、それを識別する数値。 A*スレッド*プログラムのどの部分を識別するオブジェクトが実行されています。 各スレッドは、ID、それを識別する番号を持っています。

プロセスでは、複数のスレッドがあります。 スレッドの目的は、プロセッサ時間を割り当てることです。 1 つのプロセッサを搭載したコンピューターは、複数のスレッドを割り当てることができるが、一度に 1 つのスレッドを実行できます。 各スレッドでは、短時間のみは実行され、錯覚を 1 つ以上のものが一度に行われていることをユーザーに提供、次のスレッド実行が渡されたし。 1 つ以上のプロセッサを搭載したコンピューターは、真のマルチ スレッドが行われます。 アプリケーションは、複数のスレッドが、スレッドが別のプロセッサで同時に実行できます。

Windows カーネル モード プロセスとスレッド マネージャーは、プロセス内のすべてのスレッドの実行を処理します。 1 つのプロセッサがあったり、詳細、優れた注意が必要でドライバーのプログラミング、プロセスのすべてのスレッドは、順序に関係なく、スレッドが処理されるように設計されているかどうかを確認するかどうか、ドライバーは正しく動作します。

異なるプロセスのスレッドが同時に同じリソースを使用しようとすると、問題が発生することができます。 Windows では、この問題を回避するためにいくつかの手法を提供します。 異なるプロセスのスレッドには、同じリソースが接触しないことを確認する方法と呼びます*同期*します。 同期の詳細については、次を参照してください。[同期手法](synchronization-techniques.md)します。

プロセスおよびスレッド マネージャーに直接インターフェイスを提供するルーチンには文字で、通常、プレフィックス"**Ps**"。 たとえば、 **PsCreateSystemThread**します。 Ddi カーネルの一覧は、次を参照してください。 [Windows カーネル](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_kernel/)します。

この一連のガイドラインは、これらのコールバック ルーチンに適用されます。

[_PCREATE_PROCESS_NOTIFY_ROUTINE_](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-pcreate_process_notify_routine)

[_PCREATE_PROCESS_NOTIFY_ROUTINE_EX_](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-pcreate_process_notify_routine_ex)

[_PCREATE_THREAD_NOTIFY_ROUTINE_](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-pcreate_thread_notify_routine)

[_PLOAD_IMAGE_NOTIFY_ROUTINE_](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-pload_image_notify_routine)

-    保持では、ルーチンが短く、単純に通知します。
-    プロセス、スレッド、またはイメージを検証するユーザー モード サービスへの呼び出しは使用しないでください。 
-    レジストリの呼び出しは使用しないでください。 
-    行うことをブロックまたはプロセス間通信 (IPC) しない関数呼び出し。 
-    再入デッドロックする可能性があるので、他のスレッドと同期しない操作を行います。 
-    使用[システム ワーカー スレッド](https://docs.microsoft.com/windows-hardware/drivers/kernel/system-worker-threads)をキューに作業を特に職場に関連します。 
        -    API または他のプロセスを呼び出す API が低下します。
        -    コア サービスのスレッドを中断する可能性が、ブロッキング動作します。 
-    カーネル モード スタックの使用のベスト プラクティスに注意してください。 例については、次を参照してください。[カーネル モード スタックが不足からには、ドライバーを保持する方法でしょうか。](https://docs.microsoft.com/previous-versions/windows/hardware/design/dn613940(v=vs.85))と[ドライバーの基本概念とヒント](https://docs.microsoft.com/previous-versions/windows/hardware/design/dn614604(v%3dvs.85))します。


## <a name="subsystem-processes"></a>サブシステムのプロセス


Windows 10 以降、Windows Subsystem for Linux (WSL) は、その他の Windows アプリケーションと共に、Windows でネイティブの Linux ELF64 バイナリを実行するユーザーをできます。 WSL アーキテクチャとユーザー モードとカーネル モード バイナリの実行に必要なコンポーネントについては、上の投稿を参照して、 [Windows Subsystem for Linux](https://go.microsoft.com/fwlink/p/?linkid=838012)ブログ。

コンポーネントの 1 つは、*サブシステム プロセス*bin/bash など、ユーザー モードの変更されていない Linux バイナリをホストします。 サブシステムのプロセスでは、プロセスの環境ブロック (PEB) やスレッドの終了) などの Win32 プロセスに関連付けられているデータ構造は含まれません。 サブシステムのプロセスでは、システムの呼び出しとユーザー モード例外は、ペアになっているドライバーにディスパッチされます。

変更をここでは、[プロセスとスレッド マネージャー ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff559917)サブシステム プロセスをサポートするには。

-   WSL 型がで示される、 **SubsystemInformationTypeWSL**値、 [**サブシステム\_情報\_型**](https://msdn.microsoft.com/library/windows/hardware/mt805892)列挙体。 ドライバーを呼び出すことができます[ **NtQueryInformationProcess** ](https://msdn.microsoft.com/library/windows/desktop/ms684280)と[ **NtQueryInformationThread** ](https://msdn.microsoft.com/library/windows/desktop/ms684283)を基になるサブシステムを判断します。 これらの呼び出しを返す**SubsystemInformationTypeWSL** WSL の。
-   その他のカーネル モード ドライバーできますについて通知を受け取るサブシステム プロセスの作成/削除をコールバック ルーチンを登録することによって、 [ **PsSetCreateProcessNotifyRoutineEx2** ](https://msdn.microsoft.com/library/windows/hardware/mt805891)呼び出します。 スレッドの作成/削除に関する通知を取得するドライバーを呼び出すことができます[ **PsSetCreateThreadNotifyRoutineEx**](https://msdn.microsoft.com/library/windows/hardware/dn957857)、し、指定**PsCreateThreadNotifySubsystems**として通知の種類。
-   [ **PS\_作成\_通知\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff559960)構造が拡張されており、 **IsSubsystemProcess**メンバーですWin32 以外のサブシステムを示します。 他のメンバーなど、 **FileObject**、 **ImageFileName**、 **CommandLine**サブシステム プロセスに関する追加情報を示します。 これらのメンバーの動作については、次を参照してください。 [**サブシステム\_情報\_型**](https://msdn.microsoft.com/library/windows/hardware/mt805892)します。

 

 




