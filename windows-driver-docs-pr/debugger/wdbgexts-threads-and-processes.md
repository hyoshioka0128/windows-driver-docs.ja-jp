---
title: WdbgExts のスレッドとプロセス
description: WdbgExts のスレッドとプロセス
ms.assetid: fa513435-ea91-4dc5-9488-85087d585f96
keywords:
- WdbgExts 拡張機能、スレッド
- WdbgExts 拡張機能、プロセス
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: b492274ada2ba7310748f18562da7bb8e691fb59
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838791"
---
# <a name="wdbgexts-threads-and-processes"></a>WdbgExts のスレッドとプロセス


このトピックでは、WdbgExts API を使用してスレッドとプロセスを操作する方法の概要について説明します。 [デバッガーエンジン](introduction.md#debugger-engine)でのスレッドとプロセスの概要については、このドキュメントの「[デバッガーエンジンの概要](debugger-engine-overview.md)」セクションの「[スレッドとプロセス](threads-and-processes.md)」を参照してください。

### <a name="span-idthreadsspanspan-idthreadsspanthreads"></a><span id="threads"></span><span id="THREADS"></span>レッド

現在のスレッドを記述するスレッド環境ブロック (TEB) のアドレスを取得するには、 [**Gettebaddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-gettebaddress)メソッドを使用します。 カーネルモードのデバッグでは、スレッドを記述するために KTHREAD 構造体を使用することもできます。 この構造体は、 [**Getcurrentthreadaddr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-getcurrentthreadaddr)によって返されます (ユーザーモードのデバッグでは、 **GETCURRENTTHREADADDR**は TEB のアドレスを返します)。

[スレッドコンテキスト](scopes-and-symbol-groups.md#thread-context)は、スレッドを切り替えるときに Windows によって保持される状態です。これはコンテキスト構造によって表されます。 この構造はオペレーティングシステムとプラットフォームによって異なります。コンテキスト構造を使用する場合は注意が必要です。 スレッドコンテキストは[**GetContext**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff545736(v=vs.85))関数によって返され、 [**SetContext**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556644(v=vs.85))関数を使用して設定できます。

現在のスレッドのスタックトレースを確認するには、 [**StackTrace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nc-wdbgexts-pwindbg_stacktrace_routine)関数を使用します。 スタックトレースの検査に使用されるスレッドを一時的に変更するには、 [**Setthreadforoperation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-setthreadforoperation)関数または[**SetThreadForOperation64**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-setthreadforoperation64)関数を使用します。 スタックを調べるためのその他の方法については、このドキュメントの「 [Using The Debugger ENGINE API](using-the-debugger-engine-api.md) 」セクションの「[スタックトレースの](examining-the-stack-trace.md)確認」を参照してください。

ターゲットのオペレーティングシステムスレッドに関する情報を取得するには、 [**Ioctl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nc-wdbgexts-pwindbg_ioctl_routine)操作[**IG\_使用して\_スレッド\_OS\_情報を取得**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_wdbgexts_thread_os_info)します。

### <a name="span-idprocessesspanspan-idprocessesspanprocesses"></a><span id="processes"></span><span id="PROCESSES"></span>プロセス

現在のプロセスを説明するプロセス環境ブロック (PEB) のアドレスを取得するには、 [**Getpebaddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-getpebaddress)メソッドを使用します。 カーネルモードのデバッグでは、プロセスを説明するために KPROCESS 構造体を使用することもできます。 この構造体は、 [**Getcurrentprocessaddr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-getcurrentprocessaddr)によって返されます (ユーザーモードのデバッグでは、 **GETCURRENTPROCESSADDR**は peb のアドレスを返します)。

[**GetCurrentProcessHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects-getcurrentprocesshandle)メソッドは、現在のプロセスのシステムハンドルを返します。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

より強力なスレッド操作とプロセス操作 API については、このドキュメントの「[デバッガーエンジン API を使用して](using-the-debugger-engine-api.md)、で[スレッドとプロセスを制御](controlling-threads-and-processes.md)する」を参照してください。

 

 





