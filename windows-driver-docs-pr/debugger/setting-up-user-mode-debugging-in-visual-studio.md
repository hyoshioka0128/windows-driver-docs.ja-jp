---
title: Visual Studio でのユーザーモード デバッグの設定
description: 2 つのユーザー モード デバッガーは、Microsoft Visual Studio 環境で使用できます。
ms.assetid: D36220DF-1ACB-4D8B-BC4C-1A6FCB54CA15
ms.date: 05/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5ca46bafc45a4a507148ccbf049c2d5caef408e7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574622"
---
# <a name="span-iddebuggersettingupuser-modedebugginginvisualstudiospansetting-up-user-mode-debugging-in-visual-studio"></a><span id="debugger.setting_up_user-mode_debugging_in_visual_studio"></span>Visual Studio でのユーザー モード デバッグのセットアップ


2 つのユーザー モード デバッガーは、Microsoft Visual Studio 環境で使用できます。 Windows のツールのデバッグに含まれている Windows ユーザー モード デバッガーは 1 つです。 もう 1 つは Visual Studio デバッガーで、Visual Studio 製品の一部です。 このトピックでは、Visual Studio 環境内から Windows ユーザー モード デバッガーを使用して設定する方法を説明します。

> [!IMPORTANT]
> この機能は、Windows 10 バージョン 1507、以降のバージョンの WDK でご利用いただけません。
>

## <a name="span-iddebuggingauser-modeprocessonthelocalcomputerspanspan-iddebuggingauser-modeprocessonthelocalcomputerspanspan-iddebuggingauser-modeprocessonthelocalcomputerspandebugging-a-user-mode-process-on-the-local-computer"></a><span id="Debugging_a_User-Mode_Process_on_the_Local_Computer"></span><span id="debugging_a_user-mode_process_on_the_local_computer"></span><span id="DEBUGGING_A_USER-MODE_PROCESS_ON_THE_LOCAL_COMPUTER"></span>ローカル コンピューターのユーザー モード プロセスのデバッグ


特別な設定は、ローカル コンピューター上のユーザー モード プロセスをデバッグするために必要ありません。 プロセスにアタッチまたはデバッガーでプロセスの起動については、[ユーザー モード プロセスを使用して Visual Studio のデバッグ](debugging-a-user-mode-process-using-visual-studio.md)を参照してください。

## <a name="span-iddebuggingauser-modeprocessonatargetcomputerspanspan-iddebuggingauser-modeprocessonatargetcomputerspanspan-iddebuggingauser-modeprocessonatargetcomputerspandebugging-a-user-mode-process-on-a-target-computer"></a><span id="Debugging_a_User-Mode_Process_on_a_Target_Computer"></span><span id="debugging_a_user-mode_process_on_a_target_computer"></span><span id="DEBUGGING_A_USER-MODE_PROCESS_ON_A_TARGET_COMPUTER"></span>ターゲット コンピューター上のユーザー モード プロセスのデバッグ


場合によっては、2 台のコンピューターがデバッグに使用されます。 デバッガーを実行する、*ホスト コンピューター*、されているコードの実行をデバッグして、*ターゲット コンピューター*します。 (ホスト コンピューターで実行されている) Visual Studio では、ターゲット コンピューター上のユーザー モード プロセスにアタッチする Windows ユーザー モードのデバッガーを使用できます。

対象のコンピューターに移動**コントロール パネルの &gt;ネットワークとインターネット&gt;ネットワークと共有センター&gt;共有の詳細設定**します。 **ゲストまたはパブリック**を選択します**ネットワーク探索を有効に**と**ファイルとプリンターの共有を有効に**します。

残りのホスト コンピューターから構成を行うことができます。

1.  Visual Studio で、ホスト コンピューター上で、**ツール**] メニューの [選択**プロセスにアタッチ**します。
2.  **トランスポート**、選択**Windows ユーザー モード デバッガー**します。
3.  右側に、**修飾子**ボックスで、、**参照**ボタンをクリックします。
4.  **[追加]** ボタンをクリックします。
5.  ターゲット コンピューターの名前を入力します。
6.  右側に**ターゲット コンピューターの構成**、クリックして、**構成**ボタンをクリックします。 **ターゲット コンピューターの構成** ダイアログ ボックスが開き、構成の進行状況が表示されます。
7.  構成が完了すると場合、**コンピューターを構成**ダイアログ ボックスで、をクリックして **[ok]** します。

 

 





