---
title: コントロールの GUID をトレース セッションを作成します。
description: コントロールの GUID をトレース セッションを作成します。
ms.assetid: a651ac6b-9ae0-46b0-8180-59d70ceb57fe
keywords:
- コントロール Guid WDK
- Guid の WDK ソフトウェア トレース
- 識別子の WDK ソフトウェア トレース
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16c40c4bbf3f20d82ba2269d5099e170d100635a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535394"
---
# <a name="creating-a-trace-session-with-a-control-guid"></a>コントロールの GUID をトレース セッションを作成します。


トレース セッションを作成するには入力または貼り付けることにより、[コントロール GUID](control-guid.md)トレースのプロバイダーと検索、[トレース メッセージの形式 (.tmf) ファイル](trace-message-format-file.md)そのメッセージのです。

### <a name="span-idtocreateatracesessionbytypingorpastingthecontrolguidspanspan-idtocreateatracesessionbytypingorpastingthecontrolguidspanto-create-a-trace-session-by-typing-or-pasting-the-control-guid"></a><span id="to_create_a_trace_session_by_typing_or_pasting_the_control_guid"></span><span id="TO_CREATE_A_TRACE_SESSION_BY_TYPING_OR_PASTING_THE_CONTROL_GUID"></span>入力するか、コントロールの GUID を貼り付けしてトレース セッションを作成するには

1.  [Traceview で開始](starting-and-exiting-traceview.md)します。

2.  **ファイル** メニューのをクリックして**Create New Log Session**します。

3.  クリックして**プロバイダーを追加する**します。

4.  クリックして**コントロール GUID を手動で入力した**入力するか、コントロールの GUID を貼り付けます。

5.  次のいずれかの操作を行います。

6.  -   1 つまたは複数の TMF ファイルを指定するには、次のようにクリックします。 **TMF ファイルの選択**、 をクリック**ok**、 をクリック**追加**、を参照し、ディレクトリから 1 つ以上の TMF ファイルを選択します。 別のディレクトリから TMF ファイルを選択する をクリックして、**追加**もう一度ボタンをクリックします。 それ以外の場合、をクリックして**完了**します。
    -   Traceview で指定したディレクトリ内の TMF ファイルを検索するを指示するには、次のようにクリックします。 **TMF 検索パスの設定**、 をクリック**ok**で、ディレクトリを参照し、順にクリックします**OK**。

7.  追加のプロバイダーを追加するには、クリックして**プロバイダーの追加**します。 この手順は省略可能です。

8.  **[次へ]** をクリックします。

9.  [フラグとレベルを選択します。](selecting-flags-and-levels.md)必要な場合、します。

10. [基本的なトレース セッションのオプションを設定](setting-basic-trace-session-options.md)必要な場合、します。

11. [詳細トレース セッションのオプションを設定する](setting-advanced-trace-session-options.md)必要な場合、します。

12. **[Finish]**(完了) をクリックします。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

Traceview では、トレース プロバイダーを TMF ファイルを見つけられない場合のプロバイダーの一覧のトレース プロバイダーを追加していない、 **Create New Log Session**  ダイアログ ボックスと、プロバイダーを追加したいない理由を説明するメッセージを表示しません。 プロバイダーの一覧で、プロバイダーが表示されない場合、プロシージャを再起動し、使用して、 **TMF ファイルの選択**メソッドの代わりに**TMF 検索パスの設定**します。 プロバイダーは、PDB ファイルまたは TMF ファイルを見つけられない場合、traceview でを使用してトレース セッションを作成することはできません。

使用することができますを入力するか、コントロールの GUID を貼り付け、トレース セッションを作成するときに、**トレース フラグとレベルの選択** ダイアログ ボックス (に記載されている[フラグを選択してレベル](selecting-flags-and-levels.md)) traceview でができる場合にのみプロバイダーや (TMF 検索パスの設定オプションを使用して指定された) TMF パス、プロバイダーのトレース メッセージのコントロール (.tmc) ファイルを検索できる場合は、PDB シンボル ファイルを検索します。

TMC ファイルが利用できない場合することができます、トレース フラグとレベルのプロバイダーの設定に手動で、**トレース セッション オプションの高度な** ダイアログ ボックス。 手順については、次を参照してください。[トレース セッション オプションの高度な設定](setting-advanced-trace-session-options.md)します。

TMF ファイルを指定する方法の詳細については、TMF 検索パスの設定と TMF ファイル オプションの選択を参照してください。

 

 





