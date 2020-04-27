---
title: Windows カーネル モード プロセスとスレッド マネージャー
description: Windows カーネル モード プロセスとスレッド マネージャー
ms.assetid: 4053c73e-190d-4ffe-8db2-f531d120ba81
ms.localizationpriority: High
ms.date: 10/17/2018
ms.openlocfilehash: 45a1cc4822a98ef0c9cbd3b1528c215dcfe517fc
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "72835713"
---
# <a name="windows-kernel-mode-process-and-thread-manager"></a>Windows カーネル モード プロセスとスレッド マネージャー


*プロセス*は、Windows で現在実行されているソフトウェア プログラムです。 すべてのプロセスには ID があり、それを識別する番号が付いています。 *スレッド*は、プログラムのどの部分が実行されているかを識別するオブジェクトです。 各スレッドには、それを識別する番号である ID があります。

1 つのプロセスが複数のスレッドを持つ場合があります。 スレッドの目的は、プロセッサ時間を割り当てることです。 1 つのプロセッサが搭載されたマシンには、複数のスレッドを割り当てることができますが、一度に実行できるスレッドは 1 つだけです。 各スレッドは短時間しか実行されず、実行は次のスレッドに渡され、複数のことが同時に発生しているかのような錯覚をユーザーに与えます。 複数のプロセッサが搭載されたマシンでは、本当の意味でマルチスレッドを行うことができます。 アプリケーションに複数のスレッドがある場合、スレッドを異なるプロセッサで同時に実行できます。

Windows のカーネルモード プロセスとスレッド マネージャーでは、プロセス内のすべてのスレッドの実行が処理されます。 プロセッサが 1 つでも複数でも、ドライバーのプログラミングには細心の注意を払い、スレッドの処理順序に関係なくドライバーが適切に動作するように、プロセスのすべてのスレッドを設計する必要があります。

異なるプロセスのスレッドが同時に同じリソースを使用しようとすると、問題が発生する可能性があります。 Windows には、この問題を回避するための方法がいくつか用意されています。 異なるプロセスのスレッドが同じリソースを操作しないようにする手法は、*同期*と呼ばれます。 同期の詳細については、「[同期の手法](synchronization-techniques.md)」を参照してください。

プロセスおよびスレッド マネージャーへの直接のインターフェイスを提供するルーチンには、通常、"**Ps**" という文字が先頭に付きます。たとえば、**PsCreateSystemThread** です。 カーネル DDI の一覧については、「[Windows カーネル](https://docs.microsoft.com/windows-hardware/drivers/ddi/_kernel/)」を参照してください。

この一連のガイドラインは、次のコールバック ルーチンに適用されます。

[_PCREATE_PROCESS_NOTIFY_ROUTINE_](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nc-ntddk-pcreate_process_notify_routine)

[_PCREATE_PROCESS_NOTIFY_ROUTINE_EX_](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nc-ntddk-pcreate_process_notify_routine_ex)

[_PCREATE_THREAD_NOTIFY_ROUTINE_](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nc-ntddk-pcreate_thread_notify_routine)

[_PLOAD_IMAGE_NOTIFY_ROUTINE_](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nc-ntddk-pload_image_notify_routine)

-    通知ルーチンを短時間で簡単に保持します。
-    プロセス、スレッド、またはイメージを検証するためにユーザー モード サービスを呼び出さないでください。 
-    レジストリを呼び出さないでください。 
-    ブロックやプロセス間通信 (IPC) 関数を呼び出さないでください。 
-    再入デッドロックが発生する可能性があるため、他のスレッドと同期しないでください。 
-    [システム ワーカー スレッド](https://docs.microsoft.com/windows-hardware/drivers/kernel/system-worker-threads)を使用して、特に関連する作業をキューに格納します。 
        -    遅い API または他のプロセスを呼び出す API。
        -    コア サービスのスレッドを中断する可能性のあるブロッキング動作。 
-    カーネル モード スタックの使用に関するベスト プラクティスを考慮します。 例については、「[ドライバーがカーネルモード スタックを使い果たさないようにする方法](https://docs.microsoft.com/previous-versions/windows/hardware/design/dn613940(v=vs.85))」と「[主なドライバーの概念とヒント](https://docs.microsoft.com/previous-versions/windows/hardware/design/dn614604(v=vs.85))」を参照してください。


## <a name="subsystem-processes"></a>サブシステム プロセス


Windows 10 以降、Linux 用 Windows サブシステム (WSL) を使用すると、他の Windows アプリケーションと共に、Windows 上でネイティブの Linux ELF64 バイナリを実行できるようになりました。 バイナリの実行に必要な WSL アーキテクチャと、ユーザー モードとカーネル モードのコンポーネントの詳細については、[Windows Subsystem for Linux](https://go.microsoft.com/fwlink/p/?linkid=838012) ブログの投稿を参照してください。

コンポーネントの 1 つは、/bin/bash などの変更されていないユーザーモード Linux バイナリをホストする*サブシステム プロセス*です。 サブシステム プロセスには、プロセス環境ブロック (PEB) やスレッド環境ブロック (TEB) などの Win32 プロセスに関連付けられたデータ構造が含まれていません。 サブシステム プロセスの場合、システム コールとユーザー モードの例外はペアのドライバーにディスパッチされます。

サブシステム プロセスをサポートするための[プロセスとスレッド マネージャーのルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)のページの変更点は次のとおりです。

-   WSL の種類は [**SUBSYSTEM\_INFORMATION\_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ne-ntddk-_subsystem_information_type) 列挙型の **SubsystemInformationTypeWSL** 値で示されます。 ドライバーでは [**NtQueryInformationProcess**](https://docs.microsoft.com/windows/desktop/api/winternl/nf-winternl-ntqueryinformationprocess) と [**NtQueryInformationThread**](https://docs.microsoft.com/windows/desktop/api/winternl/nf-winternl-ntqueryinformationthread) を呼び出して基礎となるサブシステムを決定できます。 これらの呼び出しからは、WSL の **SubsystemInformationTypeWSL** が返されます。
-   他のカーネル モード ドライバーでは、[**PsSetCreateProcessNotifyRoutineEx2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-pssetcreateprocessnotifyroutineex2) の呼び出しを介してコールバック ルーチンを登録することにより、サブシステム プロセスの作成/削除について通知を受け取ることができます。 スレッドの作成/削除に関する通知を受け取るには、ドライバーで [**PsSetCreateThreadNotifyRoutineEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-pssetcreatethreadnotifyroutineex) を呼び出し、通知の種類として **PsCreateThreadNotifySubsystems** を指定できます。
-   [**PS\_CREATE\_NOTIFY\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_ps_create_notify_info) 構造は、Win32 以外のサブシステムを示す **IsSubsystemProcess** メンバーを含むように拡張されました。 **FileObject**、**ImageFileName**、**CommandLine** などの他のメンバーは、サブシステム プロセスに関する追加情報を示します。 これらのメンバーの動作については、[**SUBSYSTEM\_INFORMATION\_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ne-ntddk-_subsystem_information_type) のページを参照してください。

 

 




