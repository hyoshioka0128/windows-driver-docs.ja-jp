---
title: CTL ファイルでのトレース セッションの作成
description: CTL ファイルでのトレース セッションの作成
ms.assetid: aa9aee7b-d0d2-44fe-a124-3594078a8e6c
keywords:
- コントロール Guid WDK
- .ctl ファイル
- ctl ファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4bc6cf38da8435feff70cbd7a554dea11f496d00
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571926"
---
# <a name="creating-a-trace-session-with-a-ctl-file"></a>CTL ファイルでのトレース セッションの作成


## <span id="ddk_create_a_trace_session_with_a_ctl_file_tools"></span><span id="DDK_CREATE_A_TRACE_SESSION_WITH_A_CTL_FILE_TOOLS"></span>


配置することによりトレース セッションを作成することができます、[コントロール GUID (.ctl) ファイル](control-guid-file.md)トレース プロバイダーの検索して、[トレース メッセージの形式 (.tmf) ファイル](trace-message-format-file.md)メッセージにします。

### <a name="span-idtocreateatracesessionwithactlfilespanspan-idtocreateatracesessionwithactlfilespanto-create-a-trace-session-with-a-ctl-file"></a><span id="to_create_a_trace_session_with_a_ctl_file"></span><span id="TO_CREATE_A_TRACE_SESSION_WITH_A_CTL_FILE"></span>CTL ファイルを使用してトレース セッションを作成するには

1.  [Traceview で開始](starting-and-exiting-traceview.md)します。

2.  **ファイル** メニューのをクリックして**Create New Log Session**します。

3.  クリックして**プロバイダーを追加する**します。

4.  をクリックして**CTL (コントロールの GUID) ファイル**へのパスを入力し、[制御 GUID ファイル](control-guid-file.md)はトレース プロバイダーのまたは、省略記号ボタンをクリックします (**.**)、ファイルに移動します。

5.  次のいずれかの操作を行います。
    -   1 つまたは複数の TMF ファイルを指定するには、次のようにクリックします。 **TMF ファイルの選択**、 をクリック**ok**、 をクリック**追加**、を参照し、ディレクトリから 1 つ以上の TMF ファイルを選択します。 別のディレクトリから TMF ファイルを選択する をクリックして、**追加**もう一度ボタンをクリックします。 それ以外の場合、をクリックして**完了**します。
    -   Traceview で指定したディレクトリ内の TMF ファイルを検索するを指示するには、次のようにクリックします。 **TMF 検索パスの設定**、 をクリック**ok**で、ディレクトリを参照し、順にクリックします**OK**。

6.  追加のプロバイダーを追加するには、クリックして**プロバイダーの追加**します。 この手順は省略可能です。

7.  **[次へ]** をクリックします。

8.  [フラグとレベルを選択します。](selecting-flags-and-levels.md)必要な場合、します。

9.  [基本的なトレース セッションのオプションを設定](setting-basic-trace-session-options.md)必要な場合、します。

10. [詳細トレース セッションのオプションを設定する](setting-advanced-trace-session-options.md)必要な場合、します。

11. **[完了]** をクリックします。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

Traceview では、トレース プロバイダーを TMF ファイルを見つけられない場合のプロバイダーの一覧のトレース プロバイダーを追加していない、 **Create New Log Session**  ダイアログ ボックスと、プロバイダーを追加したいない理由を説明するメッセージを表示しません。 プロバイダーの一覧で、プロバイダーが表示されない場合、プロシージャを再起動し、使用して、 **TMF ファイルの選択**メソッドの代わりに**TMF 検索パスの設定**します。 プロバイダーは、PDB ファイルまたは TMF ファイルを見つけられない、プロバイダーとトレース セッションを作成する traceview でを使うことはできません。

".Ctl"以外のファイル名拡張子を持つファイルを使用できる、 **CTL (コントロールの GUID) ファイル**オプション。 Traceview では、ファイルが、各コントロールの GUID が、ファイルの行ごとに表示されるテキスト ファイルであること、およびコントロールの GUID が、行の最初のテキストのみ必要です。 別の形式でファイルを送信する場合、traceview では、ファイルを受け入れますが、正しく指定されていないプロバイダーを有効にしません。

制御 GUID ファイルは、複数のコントロールの Guid を含めることができます。 Traceview でによりすべてのプロバイダー コントロール ファイルの Guid が表示されます。

コントロールの GUID をトレース セッションを作成するときに使用できます、**トレース フラグとレベル選択** ダイアログ ボックス (に記載されている[フラグを選択してレベル](selecting-flags-and-levels.md)) traceview でがときに、PDB に見つけることができますのみシンボル ファイルは、プロバイダー、または (TMF 検索パスの設定オプションを使用して指定された) TMF パス、プロバイダーのトレース メッセージのコントロール (.tmc) ファイルを検索できます。

TMC ファイルが利用できない場合することができます、トレース フラグとレベルのプロバイダーの設定に手動で、**トレース セッション オプションの高度な** ダイアログ ボックス。 手順については、次を参照してください。[トレース セッション オプションの高度な設定](setting-advanced-trace-session-options.md)します。

TMF ファイルを指定する方法の詳細については、TMF ファイルの選択および TMF 検索パスの設定を参照してください。

 

 





