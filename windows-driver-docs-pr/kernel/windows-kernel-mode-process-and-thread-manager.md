---
title: Windows カーネル モード プロセスとスレッド マネージャー
description: Windows カーネル モード プロセスとスレッド マネージャー
ms.assetid: 4053c73e-190d-4ffe-8db2-f531d120ba81
ms.localizationpriority: High
ms.date: 10/17/2018
ms.openlocfilehash: e494f2d3021733363fd9bea8b8a312798473e53f
ms.sourcegitcommit: c73954a5909ec8c7e189f77fd5813f2eb749687c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007581"
---
# <a name="windows-kernel-mode-process-and-thread-manager"></a>Windows カーネル モード プロセスとスレッド マネージャー


*プロセス*は、Windows で現在実行されているソフトウェアプログラムです。 すべてのプロセスには ID があり、それを識別する番号が付いています。 *スレッド*は、プログラムのどの部分が実行されているかを識別するオブジェクトです。 各スレッドには、ID を識別する番号があります。

1つのプロセスに複数のスレッドを含めることができます。 スレッドの目的は、プロセッサ時間を割り当てることです。 1つのプロセッサを搭載したコンピューターでは、複数のスレッドを割り当てることができますが、一度に実行できるスレッドは1つだけです。 各スレッドは短時間のみ実行され、次のスレッドに実行が渡されます。これにより、ユーザーは複数の処理が同時に発生していると錯覚します。 複数のプロセッサを搭載したコンピューターでは、真のマルチスレッドが発生する可能性があります。 アプリケーションに複数のスレッドがある場合、スレッドは異なるプロセッサで同時に実行できます。

Windows のカーネルモードプロセスとスレッドマネージャーは、プロセス内のすべてのスレッドの実行を処理します。 1つ以上のプロセッサがあるかどうかにかかわらず、プロセスのすべてのスレッドがどのような順序で処理されるかに関係なく、ドライバーのプログラミングで十分に注意する必要があります。

異なるプロセスのスレッドが同時に同じリソースを使用しようとすると、問題が発生する可能性があります。 Windows には、この問題を回避するための方法がいくつか用意されています。 異なるプロセスのスレッドが同じリソースを操作しないようにするための手法は、*同期*と呼ばれます。 同期の詳細については、「[同期の手法](synchronization-techniques.md)」を参照してください。

プロセスとスレッドマネージャーに直接インターフェイスを提供するルーチンには、通常、文字 "**Ps**" が付いています。たとえば、 **PsCreateSystemThread**のようになります。 カーネル DDIs の一覧については、「 [Windows カーネル](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_kernel/)」を参照してください。

この一連のガイドラインは、次のコールバックルーチンに適用されます。

[_PCREATE_PROCESS_NOTIFY_ROUTINE_](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-pcreate_process_notify_routine)

[_PCREATE_PROCESS_NOTIFY_ROUTINE_EX_](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-pcreate_process_notify_routine_ex)

[_PCREATE_THREAD_NOTIFY_ROUTINE_](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-pcreate_thread_notify_routine)

[_PLOAD_IMAGE_NOTIFY_ROUTINE_](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-pload_image_notify_routine)

-    通知ルーチンを短時間で簡単に保持します。
-    プロセス、スレッド、またはイメージを検証するために、ユーザーモードサービスを呼び出すことは避けてください。 
-    レジストリを呼び出すことはできません。 
-    ブロッキングやプロセス間通信 (IPC) 関数の呼び出しを行わないでください。 
-    再入デッドロックが発生する可能性があるため、他のスレッドと同期しないでください。 
-    [システムワーカースレッド](https://docs.microsoft.com/windows-hardware/drivers/kernel/system-worker-threads)を使用して、特に関係する作業をキューに置いてください。 
        -    他のプロセスを呼び出す遅い API または API。
        -    コアサービスでスレッドを中断する可能性のあるブロッキング動作。 
-    カーネルモードスタックの使用方法については、よく検討をお勧めします。 例については、「[ドライバーがカーネルモードスタックから実行さ](https://docs.microsoft.com/previous-versions/windows/hardware/design/dn613940(v=vs.85))れないようにする操作方法」および「[ドライバーの概念とヒント](https://docs.microsoft.com/previous-versions/windows/hardware/design/dn614604(v=vs.85))」を参照してください。


## <a name="subsystem-processes"></a>サブシステムプロセス


Windows 10 以降では、Windows Subsystem for Linux (WSL) を使用して、ユーザーは windows 上でネイティブ Linux ELF64 バイナリを他の Windows アプリケーションと共に実行できます。 WSL アーキテクチャと、バイナリの実行に必要なユーザーモードとカーネルモードのコンポーネントの詳細については、 [Windows Subsystem For Linux](https://go.microsoft.com/fwlink/p/?linkid=838012)の投稿に関するブログを参照してください。

コンポーネントの1つは、変更されていないユーザーモードの Linux バイナリ (/bin/bash など) をホストする*サブシステムプロセス*です。 サブシステムプロセスには、プロセス環境ブロック (PEB) やスレッド環境ブロック (TEB) などの Win32 プロセスに関連付けられたデータ構造が含まれていません。 サブシステムプロセスでは、システムコールとユーザーモードの例外がペアのドライバーにディスパッチされます。

次に、サブシステムプロセスをサポートするために[プロセスとスレッドマネージャールーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)を変更する方法を示します。

-   WSL 型は、[**サブシステム @ no__t-3INFORMATION @ no__t-4type**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ne-ntddk-_subsystem_information_type)列挙の**Subsysteminformationtypewsl**値によって示されます。 ドライバーは、 [**Ntqueryinformationprocess**](https://docs.microsoft.com/windows/desktop/api/winternl/nf-winternl-ntqueryinformationprocess)および[**Ntqueryinformationprocess**](https://docs.microsoft.com/windows/desktop/api/winternl/nf-winternl-ntqueryinformationthread)を呼び出して、基になるサブシステムを特定できます。 これらの呼び出しは WSL の**Subsysteminformationtypewsl**を返します。
-   その他のカーネルモードドライバーは、 [**PsSetCreateProcessNotifyRoutineEx2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-pssetcreateprocessnotifyroutineex2)呼び出しを使用してコールバックルーチンを登録することによって、サブシステムのプロセスの作成または削除に関する通知を受けることができます。 スレッドの作成または削除に関する通知を取得するために、ドライバーは[**PsSetCreateThreadNotifyRoutineEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-pssetcreatethreadnotifyroutineex)を呼び出し、通知の種類として**PsCreateThreadNotifySubsystems**を指定できます。
-   [**PS @ no__t-2CREATE @ no__t-3NOTIFY @ no__t-4INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_ps_create_notify_info)構造体が拡張され、Win32 以外のサブシステムを示す**Issubsystemprocess**メンバーが含まれるようになりました。 **FileObject**、 **imagefilename**、 **CommandLine**などの他のメンバーは、サブシステムプロセスに関する追加情報を示します。 これらのメンバーの動作の詳細については、「 [**SUBSYSTEM @ no__t-2INFORMATION @ no__t-3TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ne-ntddk-_subsystem_information_type)」を参照してください。

 

 




