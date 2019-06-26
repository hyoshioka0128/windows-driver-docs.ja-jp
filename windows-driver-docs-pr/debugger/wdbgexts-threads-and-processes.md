---
title: WdbgExts のスレッドとプロセス
description: WdbgExts のスレッドとプロセス
ms.assetid: fa513435-ea91-4dc5-9488-85087d585f96
keywords:
- スレッド、WdbgExts 拡張機能
- プロセス、WdbgExts 拡張機能
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: df35464621486bccbb32b1eea285ed2bf5540f5f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369417"
---
# <a name="wdbgexts-threads-and-processes"></a>WdbgExts のスレッドとプロセス


このトピックではスレッドとプロセスをする方法の概要、WdbgExts API を使用して操作します。 スレッドおよびプロセスの概要については、[デバッガー エンジン](introduction.md#debugger-engine)を参照してください[スレッドとプロセス](threads-and-processes.md)で、[デバッガー エンジンの概要](debugger-engine-overview.md)このドキュメントの「します。

### <a name="span-idthreadsspanspan-idthreadsspanthreads"></a><span id="threads"></span><span id="THREADS"></span>スレッド

現在のスレッドをについて説明します。 スレッド環境ブロック終了のアドレスを取得するメソッドを使用して[ **GetTebAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-gettebaddress)します。 カーネル モードのデバッグ、KTHREAD 構造体は、スレッドの記述に使用できるもあります。 この構造体がによって返される[ **GetCurrentThreadAddr** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-getcurrentthreadaddr) (ユーザー モードのデバッグ、 **GetCurrentThreadAddr** TEB のアドレスを返します)。

[スレッド コンテキスト](scopes-and-symbol-groups.md#thread-context)によって状態が保持切り替え時に Windows スレッド; CONTEXT 構造体によって表されます。 この構造体が、オペレーティング システムによって異なり、コンテキストの構造を使用するときに、プラットフォームと注意を実行する必要があります。 スレッド コンテキストがによって返される、 [ **GetContext** ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff545736(v=vs.85))関数を使用して設定することができます、 [ **SetContext** ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556644(v=vs.85))関数。

現在のスレッドのスタック トレースを確認するを使用して、 [ **StackTrace** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nc-wdbgexts-pwindbg_stacktrace_routine)関数。 スタック トレースを確認するために使用されるスレッドを一時的に変更するには、使用、 [ **SetThreadForOperation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-setthreadforoperation)または[ **SetThreadForOperation64** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-setthreadforoperation64)関数。 参照してください[スタック トレースを調べて](examining-the-stack-trace.md)で、[デバッガー エンジン API を使用して](using-the-debugger-engine-api.md)スタックを確認するための他の方法は、このドキュメントの「します。

ターゲットのオペレーティング システム スレッドに関する情報を取得する、 [ **Ioctl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nc-wdbgexts-pwindbg_ioctl_routine)操作[ **IG\_取得\_スレッド\_OS\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ns-wdbgexts-_wdbgexts_thread_os_info)します。

### <a name="span-idprocessesspanspan-idprocessesspanprocesses"></a><span id="processes"></span><span id="PROCESSES"></span>プロセス

プロセスを現在を説明するプロセスの環境ブロック (PEB) のアドレスを取得するには、メソッドを使用して[ **GetPebAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-getpebaddress)します。 カーネル モードのデバッグ、KPROCESS 構造はプロセスの記述に使用できるもあります。 この構造体がによって返される[ **GetCurrentProcessAddr** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-getcurrentprocessaddr) (ユーザー モードのデバッグ、 **GetCurrentProcessAddr** PEB のアドレスを返します)。

メソッド[ **GetCurrentProcessHandle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects-getcurrentprocesshandle)現在のプロセスのシステムのハンドルを返します。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

強力なスレッドの操作とプロセス操作 API では、次を参照してください。[を制御するスレッドとプロセス](controlling-threads-and-processes.md)で、[デバッガー エンジン API を使用して](using-the-debugger-engine-api.md)このドキュメントの「します。

 

 





