---
title: ローカル カーネルモード デバッグ
description: ローカル カーネルモード デバッグ
ms.assetid: e66dc23b-9254-4148-9828-d27c30bfa492
keywords:
- ローカルカーネルデバッグ
- ローカルカーネルデバッグ、使用可能なコマンド
- ローカルカーネルデバッグ、LiveKD ツール
- LiveKD ツール
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d81f3681d73140c4bf897e8c3adddc7620c4a1ec
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534449"
---
# <a name="local-kernel-mode-debugging"></a>ローカル カーネルモード デバッグ


Windows 用デバッグツールでは、*ローカルカーネルデバッグ*がサポートされています。 これは、1台のコンピューターでのカーネルモードのデバッグです。 つまり、デバッガーは、デバッグされているのと同じコンピューター上で実行されます。

## <a name="span-idstarting_local_kernel_debuggingspanspan-idstarting_local_kernel_debuggingspansetting-up-local-kernel-mode-debugging"></a><span id="starting_local_kernel_debugging"></span><span id="STARTING_LOCAL_KERNEL_DEBUGGING"></span>ローカルカーネルモードデバッグの設定


ローカルカーネルモードデバッグの設定の詳細については、「 [1 台のコンピューターのローカルカーネルモードデバッグを手動で設定する](setting-up-local-kernel-debugging-of-a-single-computer-manually.md)」を参照してください。

## <a name="span-idstarting_the_debugging_sessionspanspan-idstarting_the_debugging_sessionspanspan-idstarting_the_debugging_sessionspanstarting-the-debugging-session"></a><span id="Starting_the_Debugging_Session"></span><span id="starting_the_debugging_session"></span><span id="STARTING_THE_DEBUGGING_SESSION"></span>デバッグセッションを開始しています


### <a name="span-idusing_windbgspanspan-idusing_windbgspanspan-idusing_windbgspanusing-windbg"></a><span id="Using_WinDbg"></span><span id="using_windbg"></span><span id="USING_WINDBG"></span>WinDbg の使用

管理者として WinDbg を開きます。 [**ファイル**] メニューの [**カーネルデバッグ**] をクリックします。 [カーネルデバッグ] ダイアログボックスで、[**ローカル**] タブを開きます。 [ **OK**] をクリックします。

また、管理者としてコマンドプロンプトウィンドウを開き、次のコマンドを入力して、WinDbg を使用してセッションを開始することもできます。

**windbg-kl ダイバージェンス**

### <a name="span-idusing_kdspanspan-idusing_kdspanspan-idusing_kdspanusing-kd"></a><span id="Using_KD"></span><span id="using_kd"></span><span id="USING_KD"></span>KD の使用

管理者としてコマンドプロンプトウィンドウを開き、次のコマンドを入力します。

**kd-kl ダイバージェンス**

## <a name="span-idcommands_that_are_not_availablespanspan-idcommands_that_are_not_availablespancommands-that-are-not-available"></a><span id="commands_that_are_not_available"></span><span id="COMMANDS_THAT_ARE_NOT_AVAILABLE"></span>使用できないコマンド


すべてのコマンドがローカルカーネルデバッグセッションで使用できるわけではありません。 通常、操作を再開することはできないため、ターゲットコンピューターを一時的に停止するコマンドを使用することはできません。

特に、次のコマンドは使用できません。

-   実行コマンド ( **g (開始)**、 **p (Step)**、 **t (Trace)**、 **wt (trace And Watch Data)**、 **tb (trace To Next Branch)**、 **gh (例外を処理した状態**で実行)、および**gn (例外を処理しないで**ください)

-   **クラッシュ**、**ダンプ**、 **. reboot**などのファイルコマンドをシャットダウンおよびダンプする

-   ブレークポイントコマンド ( **bp**、 **bu**、 **ba**、 **bc**、 **bd**、 **be**、および**bl** )

-   **R**やバリエーションなどの表示コマンドを登録する

-   **K**やバリエーションなどのスタックトレースコマンド

WinDbg でローカルカーネルデバッグを実行している場合は、同等のすべてのメニューコマンドとボタンも使用できません。

## <a name="span-idcommands_that_are_availablespanspan-idcommands_that_are_availablespancommands-that-are-available"></a><span id="commands_that_are_available"></span><span id="COMMANDS_THAT_ARE_AVAILABLE"></span>使用可能なコマンド


すべてのメモリ入力および出力コマンドを使用できます。 ユーザーメモリとカーネルメモリから自由に読み取ることができます。 メモリに書き込むこともできます。 カーネルメモリの不適切な部分には書き込まないでください。データ構造が破損したり、コンピューターが応答しなくなったり (*クラッシュ*) したりする可能性があります。

## <a name="span-iddifficulties_in_performing_local_kernel_debuggingspanspan-iddifficulties_in_performing_local_kernel_debuggingspandifficulties-in-performing-local-kernel-debugging"></a><span id="difficulties_in_performing_local_kernel_debugging"></span><span id="DIFFICULTIES_IN_PERFORMING_LOCAL_KERNEL_DEBUGGING"></span>ローカルカーネルデバッグの実行に関する問題


ローカルカーネルデバッグは非常に微妙な操作です。 システムを破損したりクラッシュしたりしないように注意してください。

ローカルカーネルデバッグの最も困難な側面の1つは、コンピューターの状態が絶えず変化することです。 メモリはページングされ、アクティブなプロセスは常に変化し、仮想アドレスコンテキストは一定のままではなくなります。 ただし、これらの条件下では、特定のデバイスの状態など、変化が遅くなる項目を効果的に分析できます。

カーネルモードドライバーと Windows オペレーティングシステムでは、多くの場合、 **Dbgprint**および関連する機能を使用して、カーネルデバッガーにメッセージが送信されます。 これらのメッセージは、ローカルカーネルデバッグ中に自動的には表示されません。 これは、 [**! dbgprint**](-dbgprint.md)拡張機能を使用して表示できます。

## <a name="span-idlivekdspanspan-idlivekdspanlivekd"></a><span id="livekd"></span><span id="LIVEKD"></span>LiveKD


LiveKD ツールは、ローカルカーネルデバッグをシミュレートします。 このツールは、カーネルメモリの "スナップショット" ダンプファイルを作成します。このファイルは、このスナップショットの作成中に実際にカーネルを停止することはありません。 このため、スナップショットには、実際にはコンピューターの1つのインスタント状態が表示されない場合があります。

LiveKD は、Windows 用デバッグツールのパッケージには含まれていません。 [LiveKd](https://docs.microsoft.com/sysinternals/downloads/livekd)は、Windows Sysinternals サイトからダウンロードできます。

 

 





