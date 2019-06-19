---
title: Visual Studio を使用したユーザーモード プロセスのデバッグ
description: Microsoft Visual studio では、実行中のプロセスにアタッチまたはを生成し、新しいプロセスにアタッチする Windows ユーザー モードのデバッガーを使用できます。
ms.assetid: C19D1B6F-B97B-4C1B-AD84-AC974C5F5C8C
ms.date: 05/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8f04f48700e6a6633d84e8be61ec6bb2faedf155
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327352"
---
# <a name="span-iddebuggerdebuggingauser-modeprocessusingvisualstudiospandebugging-a-user-mode-process-using-visual-studio"></a><span id="debugger.debugging_a_user-mode_process_using_visual_studio"></span>Visual Studio を使用してユーザー モード プロセスのデバッグ

> [!IMPORTANT]
> この機能は、Windows 10 バージョン 1507、以降のバージョンの WDK でご利用いただけません。
>

Microsoft Visual studio では、実行中のプロセスにアタッチまたはを生成し、新しいプロセスにアタッチする Windows ユーザー モードのデバッガーを使用できます。 プロセスをデバッガーを実行している同じコンピューターで実行できる、または別のコンピューターで実行できます。

このトピックで示す手順では、Visual Studio に統合された Windows Driver Kit が必要です。 統合環境を取得するには、最初に、Visual Studio をインストールし、Windows Driver Kit (WDK) をインストールします。 詳細については、次を参照してください。 [Windows Driver Kit (WDK)](https://go.microsoft.com/fwlink/p?linkid=391063)します。

## <a name="span-idattachingtoarunningprocessonthesamecomputerspanspan-idattachingtoarunningprocessonthesamecomputerspanspan-idattachingtoarunningprocessonthesamecomputerspanattaching-to-a-running-process-on-the-same-computer"></a><span id="Attaching_to_a_running_process_on_the_same_computer"></span><span id="attaching_to_a_running_process_on_the_same_computer"></span><span id="ATTACHING_TO_A_RUNNING_PROCESS_ON_THE_SAME_COMPUTER"></span>同じコンピューターで実行中のプロセスにアタッチします。


1.  Visual Studio から、**ツール**] メニューの [選択**プロセスにアタッチ**します。
2.  **プロセスにアタッチ**ダイアログ ボックスで、セット**トランスポート**に**Windows ユーザー モード デバッガー**、設定と**修飾子**に**Localhost**します。
3.  **選択可能なプロセス**一覧で、プロセスにアタッチするを選択します。
4.  クリックして**アタッチ**します。

### <a name="span-idnoninvasivedebuggingspanspan-idnoninvasivedebuggingspanspan-idnoninvasivedebuggingspannoninvasive-debugging"></a><span id="Noninvasive_debugging"></span><span id="noninvasive_debugging"></span><span id="NONINVASIVE_DEBUGGING"></span>待合室デバッグ

実行中のプロセスをデバッグし、わずかに干渉するかどうか、その実行には、プロセスをデバッグする必要があります[noninvasively](noninvasive-debugging--user-mode-.md)します。

## <a name="span-idspawninganewprocessonthesamecomputerspanspan-idspawninganewprocessonthesamecomputerspanspan-idspawninganewprocessonthesamecomputerspanspawning-a-new-process-on-the-same-computer"></a><span id="Spawning_a_new_process_on_the_same_computer"></span><span id="spawning_a_new_process_on_the_same_computer"></span><span id="SPAWNING_A_NEW_PROCESS_ON_THE_SAME_COMPUTER"></span>同じコンピューター上の新しいプロセスを作成


1.  Visual Studio から、**ツール**] メニューの [選択 **デバッガーの起動**します。
2.  **デバッガーの起動 [** ] ダイアログ ボックスに、実行可能ファイルへのパスを入力します。 引数と作業ディレクトリを入力することもできます。
3.  クリックして**を起動します。**

デバッガーが (子プロセスとも呼ばれます) を作成するプロセスにデバッガーが作成していないプロセスよりも少し異なる方法で動作します。

標準ヒープ API を使用する代わりには、デバッガーが作成するプロセスは、特別なデバッグ ヒープを使用します。 使用して、デバッグ ヒープではなく標準ヒープを使用する子プロセスを強制することができます、\_いいえ\_デバッグ\_ヒープ環境変数。

また、対象アプリケーションは、デバッガーの子プロセスであるために、デバッガーのアクセス許可を継承します。 このアクセス許可には、それ以外の場合を実行できなかった特定のアクションを実行する対象のアプリケーションが有効にすることがあります。 たとえば、対象アプリケーションは保護されているプロセスを制御することにあります。

## <a name="span-idattachingtoarunningprocessonaseparatecomputerspanspan-idattachingtoarunningprocessonaseparatecomputerspanspan-idattachingtoarunningprocessonaseparatecomputerspanattaching-to-a-running-process-on-a-separate-computer"></a><span id="Attaching_to_a_running_process_on_a_separate_computer"></span><span id="attaching_to_a_running_process_on_a_separate_computer"></span><span id="ATTACHING_TO_A_RUNNING_PROCESS_ON_A_SEPARATE_COMPUTER"></span>別のコンピューターで実行中のプロセスにアタッチします。


場合があります、デバッガーとデバッグ中のコードは、別のコンピューターで実行します。 デバッガーを実行しているコンピューターが呼び出されます、*ホスト コンピューター*、デバッグ中のコードを実行するコンピューターを呼び出すと、*対象のコンピュータ*します。 ホスト コンピューターでは、Visual Studio からターゲット コンピューターを構成できます。 ターゲット コンピューターの構成と呼ばれます*プロビジョニング*対象のコンピュータ。 詳しくは、「[ドライバーの展開およびテストのためのコンピューターのプロビジョニング (WDK 8.1)](https://msdn.microsoft.com/library/windows/hardware/dn745909)」をご覧ください。

対象のコンピュータがプロビジョニングされると、ホスト コンピューター上の Visual Studio を使用して、ターゲット コンピューターで実行されているプロセスにアタッチすることができます。

1.  Visual Studio で、ホスト コンピューター上の**ツール**] メニューの [選択**プロセスにアタッチ**。
2.  **プロセスにアタッチ**ダイアログ ボックスで、セット**トランスポート**に**Windows ユーザー モード デバッガー**、設定と**修飾子**ターゲットの名前をコンピューター。
3.  **選択可能なプロセス**一覧で、プロセスにアタッチするを選択します。
4.  クリックして**アタッチ**します。

**注**  個別のホストとターゲット コンピューターを使用している場合はインストールしない Visual Studio と WDK ターゲット コンピューターにします。 Visual Studio と WDK がターゲット コンピューターにインストールされている場合、デバッグはサポートされていません。

 

 

 





