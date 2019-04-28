---
title: カーネル デバッガーからのユーザーモード デバッガーの制御
description: カーネル デバッガーからのユーザーモード デバッガーの制御
ms.assetid: 8fba2187-cf22-41ad-9b06-228a5b082822
keywords:
- KD、CDB、NTSD または制御します。
- WinDbg、CDB、NTSD または制御します。
- CDB でカーネル デバッガーへのコントロールのリダイレクト
- NTSD、カーネル デバッガーへのコントロールのリダイレクト
- カーネル デバッガーへのユーザー モードの出力のリダイレクト
- カーネル デバッガーからユーザー モード デバッガーの制御
- カーネル デバッガーからユーザー モード デバッガーの制御の概要
- カーネル デバッガー、スリープ モードからユーザー モード デバッガーの制御
- スリープ モード
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: efeb46b14ac40f36e972cb474746dfaf58f4a627
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375053"
---
# <a name="controlling-the-user-mode-debugger-from-the-kernel-debugger"></a>カーネル デバッガーからのユーザーモード デバッガーの制御


## <span id="ddk_controlling_the_user_mode_debugger_from_the_kernel_debugger_dbg"></span><span id="DDK_CONTROLLING_THE_USER_MODE_DEBUGGER_FROM_THE_KERNEL_DEBUGGER_DBG"></span>


入力と、カーネル デバッガーに、ユーザー モード デバッガーから出力をリダイレクトすることができます。 このリダイレクトは、ターゲット コンピューターで発生している特定のユーザー モードのデバッグ セッションを制御するには、カーネル デバッガーを使用できます。

KD または WinDbg のいずれかは、カーネル デバッガーとして使用できます。 WinDbg の使い慣れた機能の多くはこのシナリオでは使用できないことに注意してください。 たとえば、ローカル ウィンドウ、逆アセンブル ウィンドウまたは呼び出し履歴 ウィンドウを使用することはできませんし、ソース コードをステップすることはできません。 これは、(NTSD または CDB)、デバッガーのビューアーとして WinDbg がのみ機能するため、ターゲット コンピューターで実行します。

ユーザー モード デバッガーとして、CDB、または NTSD のいずれかを使用できます。 NTSD ことをお勧め、プロセッサとのアプリケーションのデバッグ中はコンピューターのオペレーティング システムから最小限のリソースが必要です。 実際には、カーネル デバッガーの制御下で開始されると、NTSD NTSD ウィンドウは作成されません。 NTSD をシャット ダウンにユーザー モードのデバッグ起動段階の早い段階でシリアル ポート経由と遅延を行うことができます。

**注**  、 [ **.shell** ](-shell--command-shell-.md)カーネル デバッガーに、ユーザー モード デバッガーの出力がリダイレクトされたときに、コマンドがサポートされていません。

 

このセクションで、次のとおりです。

-   [デバッグ セッションを開始する](starting-the-debugging-session.md)カーネル デバッガーからユーザー モード デバッガーが制御されているセッションを開始する方法について説明します。

-   [モードの切り替え](switching-modes.md)が関与する 4 つの異なるモードをについて説明します。 方法とそれらの間で交互に使用します。

-   [この手法を使用するタイミング](when-to-use-this-technique.md)この手法が特に役立つシナリオについて説明します。

-   [リモート デバッグで、このメソッドを組み合わせて](combining-this-method-with-remote-debugging.md)カーネル デバッガーからユーザー モード デバッガーの制御を同時にデバッグ サーバーとして使用する方法について説明します。 この組み合わせは、シンボル サーバーで、ユーザー モードのシンボルが存在する場合に役立ちます。

 

 





