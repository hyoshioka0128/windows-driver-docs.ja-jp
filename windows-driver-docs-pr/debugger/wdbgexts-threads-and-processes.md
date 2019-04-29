---
title: WdbgExts のスレッドとプロセス
description: WdbgExts のスレッドとプロセス
ms.assetid: fa513435-ea91-4dc5-9488-85087d585f96
keywords:
- スレッド、WdbgExts 拡張機能
- プロセス、WdbgExts 拡張機能
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: c597935241f37f8de494f0e59d392e22a63a4058
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325830"
---
# <a name="wdbgexts-threads-and-processes"></a>WdbgExts のスレッドとプロセス


このトピックではスレッドとプロセスをする方法の概要、WdbgExts API を使用して操作します。 スレッドおよびプロセスの概要については、[デバッガー エンジン](introduction.md#debugger-engine)を参照してください[スレッドとプロセス](threads-and-processes.md)で、[デバッガー エンジンの概要](debugger-engine-overview.md)このドキュメントの「します。

### <a name="span-idthreadsspanspan-idthreadsspanthreads"></a><span id="threads"></span><span id="THREADS"></span>スレッド

現在のスレッドをについて説明します。 スレッド環境ブロック終了のアドレスを取得するメソッドを使用して[ **GetTebAddress**](https://msdn.microsoft.com/library/windows/hardware/ff549267)します。 カーネル モードのデバッグ、KTHREAD 構造体は、スレッドの記述に使用できるもあります。 この構造体がによって返される[ **GetCurrentThreadAddr** ](https://msdn.microsoft.com/library/windows/hardware/ff545889) (ユーザー モードのデバッグ、 **GetCurrentThreadAddr** TEB のアドレスを返します)。

[スレッド コンテキスト](scopes-and-symbol-groups.md#thread-context)によって状態が保持切り替え時に Windows スレッド; CONTEXT 構造体によって表されます。 この構造体が、オペレーティング システムによって異なり、コンテキストの構造を使用するときに、プラットフォームと注意を実行する必要があります。 スレッド コンテキストがによって返される、 [ **GetContext** ](https://msdn.microsoft.com/library/windows/hardware/ff545736)関数を使用して設定することができます、 [ **SetContext** ](https://msdn.microsoft.com/library/windows/hardware/ff556644)関数。

現在のスレッドのスタック トレースを確認するを使用して、 [ **StackTrace** ](https://msdn.microsoft.com/library/windows/hardware/ff558794)関数。 スタック トレースを確認するために使用されるスレッドを一時的に変更するには、使用、 [ **SetThreadForOperation** ](https://msdn.microsoft.com/library/windows/hardware/ff556830)または[ **SetThreadForOperation64** ](https://msdn.microsoft.com/library/windows/hardware/ff556832)関数。 参照してください[スタック トレースを調べて](examining-the-stack-trace.md)で、[デバッガー エンジン API を使用して](using-the-debugger-engine-api.md)スタックを確認するための他の方法は、このドキュメントの「します。

ターゲットのオペレーティング システム スレッドに関する情報を取得する、 [ **Ioctl** ](https://msdn.microsoft.com/library/windows/hardware/ff551084)操作[ **IG\_取得\_スレッド\_OS\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff550924)します。

### <a name="span-idprocessesspanspan-idprocessesspanprocesses"></a><span id="processes"></span><span id="PROCESSES"></span>プロセス

プロセスを現在を説明するプロセスの環境ブロック (PEB) のアドレスを取得するには、メソッドを使用して[ **GetPebAddress**](https://msdn.microsoft.com/library/windows/hardware/ff548122)します。 カーネル モードのデバッグ、KPROCESS 構造はプロセスの記述に使用できるもあります。 この構造体がによって返される[ **GetCurrentProcessAddr** ](https://msdn.microsoft.com/library/windows/hardware/ff545779) (ユーザー モードのデバッグ、 **GetCurrentProcessAddr** PEB のアドレスを返します)。

メソッド[ **GetCurrentProcessHandle** ](https://msdn.microsoft.com/library/windows/hardware/ff545816)現在のプロセスのシステムのハンドルを返します。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

強力なスレッドの操作とプロセス操作 API では、次を参照してください。[を制御するスレッドとプロセス](controlling-threads-and-processes.md)で、[デバッガー エンジン API を使用して](using-the-debugger-engine-api.md)このドキュメントの「します。

 

 





