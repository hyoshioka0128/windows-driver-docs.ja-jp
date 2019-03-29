---
title: 単一コンピューターのローカル カーネル デバッグの手動設定
description: 単一コンピューターのローカル カーネル デバッグの手動設定
ms.assetid: FC717B1C-A68A-4002-A528-BFC3521C5E8A
ms.date: 07/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7c09ae58a59a182fbb01170a7402927b9dd88336
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574632"
---
# <a name="setting-up-local-kernel-debugging-of-a-single-computer-manually"></a>単一コンピューターのローカル カーネル デバッグの手動設定


デバッグ ツールの Windows サポート*ローカル カーネル デバッグ*します。 これは、1 台のコンピューターでカーネル モードのデバッグです。 つまり、デバッガーは、デバッグ中のと同じコンピューターで実行されます。 ローカル デバッグには、ことになる実行を停止する OS カーネル モード プロセスに、状態が中断しないを確認できます。

*ローカル*bcdedit オプションは、以降 Windows 8.0 および Windows Server 2012 で利用できます。

## <a name="span-idstartinglocalkerneldebuggingspanspan-idstartinglocalkerneldebuggingspansetting-up-local-kernel-mode-debugging"></a><span id="starting_local_kernel_debugging"></span><span id="STARTING_LOCAL_KERNEL_DEBUGGING"></span>ローカル カーネル モード デバッグの設定

> [!IMPORTANT]
> Bcdedit を使用してブート情報を変更する前に、テスト用のコンピューターの BitLocker とセキュア ブートなどの Windows セキュリティ機能を一時的に中断する必要があります。 セキュア ブートは、再度有効に完了したらとデバッグは無効になりましたカーネルがローカル コンピューターでデバッグします。  


1.  管理者としてコマンド プロンプト ウィンドウを開きます。 入力**の bcdedit/debug**
2.  コンピューターがデバッグ トランスポートの対象として構成されていない場合は、入力**bcdedit/dbgsettings ローカル**
3.  コンピューターを再起動します。

## <a name="span-idstartingthedebuggingsessionspanspan-idstartingthedebuggingsessionspanspan-idstartingthedebuggingsessionspanstarting-the-debugging-session"></a><span id="Starting_the_Debugging_Session"></span><span id="starting_the_debugging_session"></span><span id="STARTING_THE_DEBUGGING_SESSION"></span>デバッグ セッションの開始


### <a name="span-idusingwindbgspanspan-idusingwindbgspanspan-idusingwindbgspanusing-windbg"></a><span id="Using_WinDbg"></span><span id="using_windbg"></span><span id="USING_WINDBG"></span>WinDbg を使用します。

WinDbg を管理者として開きます。 **ファイル**] メニューの [選択**カーネル デバッグ**します。 カーネル デバッグ ダイアログ ボックスで、開く、**ローカル**タブ。**[OK]** をクリックします。

WinDbg に管理者としてコマンド プロンプト ウィンドウを開き、次のコマンドを入力してセッションを開始することもできます。

**windbg -kl**

### <a name="span-idusingkdspanspan-idusingkdspanspan-idusingkdspanusing-kd"></a><span id="Using_KD"></span><span id="using_kd"></span><span id="USING_KD"></span>KD を使用します。

管理者は、コマンド プロンプト ウィンドウを開き、次のコマンドを入力します。

**kd kl**

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[ローカル カーネル モードのデバッグ](performing-local-kernel-debugging.md)

[カーネル モードのデバッグを手動での設定](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)

 

 






