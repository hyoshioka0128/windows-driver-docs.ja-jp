---
title: トレース フラグとレベルの選択 ダイアログ ボックスを開く
description: トレース フラグとレベルの選択 ダイアログ ボックスを開く
ms.assetid: f6ee808e-ea29-492b-b161-0a3b57140214
keywords:
- WDK のトレース フラグ
- WDK ソフトウェア トレースのフラグ
- WDK のトレース レベル
- WDK ソフトウェア トレースのレベル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea90faac2f86afc3a68b03b0ab21f6f9feb634bd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553803"
---
# <a name="opening-the-tracing-flags-and-level-selection-dialog-box"></a>トレース フラグとレベルの選択 ダイアログ ボックスを開く


使用することができます、**トレース フラグとレベル選択**を選択し、セッションを作成し、セッション中に、フラグとプロバイダーのレベルを変更 ダイアログ ボックスが実行されています。

### <a name="span-idwhilecreatingatracesessionspanspan-idwhilecreatingatracesessionspanwhile-creating-a-trace-session"></a><span id="while_creating_a_trace_session"></span><span id="WHILE_CREATING_A_TRACE_SESSION"></span>トレース セッションを作成するときに

1.  [Traceview でを起動します。](starting-and-exiting-traceview.md)

2.  **ファイル** メニューのをクリックして**Create New Log Session**します。

3.  クリックして**プロバイダーの追加**プロバイダーを追加するとします。

4.  必要な場合は、追加のプロバイダーを追加.

5.  **[次へ]** をクリックします。

6.  **ログ セッション オプション** ページで、をクリックして、**フラグの設定とレベル**ボタンをクリックします。

### <a name="span-idwhileatracesessionisrunningspanspan-idwhileatracesessionisrunningspanwhile-a-trace-session-is-running"></a><span id="while_a_trace_session_is_running"></span><span id="WHILE_A_TRACE_SESSION_IS_RUNNING"></span>トレース セッションの実行中に

1.  [トレース セッション リスト](trace-session-list.md)、トレース セッションの行を検索します。

2.  検索、**フラグ**または**レベル**をクリックしてその行の列、**設定**値。 (値は**設定**セッション プロバイダーを識別するために、PDB ファイルを使用する場合)。

3.  クリックすると**設定**開きます、**トレース フラグとレベルの選択** ダイアログ ボックス。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

**フラグの設定とレベル**traceview でを検索できる場合にのみ、オプションが有効になっている、 [PDB シンボル ファイル](pdb-symbol-files.md)プロバイダーのまたはが見つかったときに、[トレース メッセージのコントロール (.tmc) ファイル](trace-message-control-file.md)用、TMF パス内のプロバイダー (を使用して指定された、 **TMF 検索パスの設定**オプション)。

 

 





