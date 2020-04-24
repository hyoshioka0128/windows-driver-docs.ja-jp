---
title: Winqual Submission Tool (winqual.exe)
description: Winqual Submission Tool (winqual.exe)
ms.assetid: f7a34ee3-0532-465b-acb0-1ff80e2d4cb8
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7273640dd6d764bd79efbdf39d6584ae62dad092
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "68917853"
---
# <a name="winqual-submission-tool-winqualexe"></a>Winqual Submission Tool (winqual.exe)


Winqual Submission Tool (Winqual.exe) を使うと、Microsoft Windows ハードウェア認定用の提出パッケージを作成できます。 このツールは、準備された提出の種類に関する情報と、提出に必要なすべてのログ、ドライバー、シンボルを収集します。

また、Winqual.exe は WLK にのみ使用できます。

## <a name="installing-the-winqual-submission-tool"></a>Winqual Submission Tool のインストール


1.  ダッシュボードに Microsoft アカウントでサインインします。

2.  左側のナビゲーション メニューの **[ドライバー]** をクリックします。 ページの下部にある **[Get the essentials]\(必須項目の取得\)** セクションで、 **[Winqual Submission Tool (WST)]** をクリックします。

3.  **[ファイルのダウンロード - セキュリティの警告]** ダイアログ ボックスで、 **[実行]** をクリックします。

4.  **[Internet Explorer - セキュリティ警告]** ダイアログ ボックスで、 **[実行]** をクリックします。

5.  **[Welcome]** (ようこそ) 画面で、 **[次へ]** をクリックします。

6.  **[License Agreement]** (使用許諾契約書) 画面で、 **[I agree]** (同意します) をクリックし、 **[Next]** (次へ) をクリックします。

7.  **[Select Installation Folder]** (インストール フォルダーの選択) 画面で、 **[Next]** (次へ) をクリックします。

8.  **[Confirm Installation]** (インストールの確認) 画面で、 **[Next]** (次へ) をクリックします。

9.  **[Close]** (閉じる) をクリックしてインストール プロセスを終了します。

## <a name="span-idhow_to_use_wstspanspan-idhow_to_use_wstspanspan-idhow_to_use_wstspanhow-to-use-wst"></a><span id="How_to_use_WST"></span><span id="how_to_use_wst"></span><span id="HOW_TO_USE_WST"></span>WST の使用方法


Windows Submission Tool (WST) を使用するには:

1.  ツールを開くと、 **[Welcome]** (ようこそ) 画面が表示されます。 次回このツールを開いたときにこのダイアログ ボックスが表示されないようにするには、 **[Don't show this message again]** (今後このメッセージを表示しない) をオンにします。 このダイアログ ボックスが再び表示されるようにするには、 **[Tools]** (ツール)、 **[Options]** (オプション) の順にクリックし、 **[Show Welcome screen on startup]** (起動時にようこそ画面を表示する) チェック ボックスをオンにします。

2.  メイン画面が表示されます。この画面では、提出パッケージを作成するためのテスト結果とドライバーを追加できます。

3.  WST の新しいバージョンが利用できる場合は、新しいバージョンをインストールするよう求めるメッセージが表示されます。

4.  バージョン チェックに失敗した場合は、警告メッセージが表示されます。このメッセージは、 **[Don't show this message again]** (今後このメッセージを表示しない) チェック ボックスをオフにすると無効にできます。

    **注**  このダイアログ ボックスが再び表示されるようにするには、 **[Tools]\(ツール\)** 、 **[Options]\(オプション\)** の順にクリックし、 **[Warn if update check fails]\(更新チェックに失敗したら警告する\)** チェック ボックスをオンにします。

     

5.  テスト結果を提出パッケージに追加し、後で使うことができるようにリストを保存します。 すべての提出情報を含む **.xml** ファイルが作成されます (このファイルは、後で提出を作成するために使います)。

6.  **[Save As]** (名前を付けて保存) メニュー項目またはツール バー ボタンを使うと、ファイルを別の名前で保存できます。

7.  保存されたファイルが **[Recent Files]** (最近使ったファイル) メニューに追加されます。

WST では、次の操作を行うこともできます。

-   **[New]** (新規作成) メニュー項目またはツール バー ボタンをクリックして、新しい提出を開始できます。

-   **[Open]** (開く) メニュー項目またはツール バー ボタンをクリックして、保存済みのファイルを開くことができます。 メニュー項目をクリックして、 **[Recent Files]** に表示されているファイルを開くことができます。

-   **[Remove]** (削除) ボタンをクリックして、一覧のエントリを個別に削除できます。すべてのエントリを一度に削除するには、 **[Remove All]** (すべて削除) をクリックします。

-   提出パッケージには、オプションの Read-me ファイル ( **.docx**、 **.doc**、 **.txt**) ファイルを含めることができます。

## <a name="span-idhow_to_create_a_systems_submission_packagespanspan-idhow_to_create_a_systems_submission_packagespanspan-idhow_to_create_a_systems_submission_packagespanhow-to-create-a-systems-submission-package"></a><span id="How_to_create_a_systems_submission_package"></span><span id="how_to_create_a_systems_submission_package"></span><span id="HOW_TO_CREATE_A_SYSTEMS_SUBMISSION_PACKAGE"></span>システム提出パッケージを作成する方法


1.  メイン画面で、 **[Add]** (追加) ボタンをクリックします。

2.  **.cpk** ファイル (WLK テスト結果) を参照し、 **[Load]** (読み込み) をクリックします。

3.  テスト結果が追加されたら、 **[Add DTM Results]** (DTM 結果の追加) ダイアログ ボックスを閉じて、情報をメイン画面に追加します。

4.  追加されたエントリを編集するには、 **[Edit]** (編集) ボタンをクリックします。 すべての情報が入力された状態で **[Edit DTM Results]** (DTM 結果の編集) ダイアログ ボックスが表示されます。

5.  すべてのエントリを追加した後で、 **[Create Submission]** (申請の作成) ボタンをクリックして提出パッケージを作成できます。

6.  パッケージの作成中にエラーを検出することができます。 エラーが検出されると、パッケージの作成は中止されます。 エラーが検出されたエントリは、赤色で強調表示されます。 エラーをもう一度表示するには、メイン ウィンドウの **[View Errors]** (エラーの表示) ボタンをクリックします。 パッケージを作成するには、すべてのエラーが修正されている必要があります。 エラーを修正するには、エントリを編集し、ドライバーまたはテスト結果を更新します。

7.  すべてのエラーを修正した後、提出パッケージを作成できます。 提出パッケージは、.xml ファイルと同じ名前で同じ場所に作成されます。

## <a name="span-idhow_to_create_a_device_submission_packagespanspan-idhow_to_create_a_device_submission_packagespanspan-idhow_to_create_a_device_submission_packagespanhow-to-create-a-device-submission-package"></a><span id="How_to_create_a_device_submission_package"></span><span id="how_to_create_a_device_submission_package"></span><span id="HOW_TO_CREATE_A_DEVICE_SUBMISSION_PACKAGE"></span>デバイス提出パッケージを作成する方法


1.  メイン画面で、 **[Add]** (追加) ボタンをクリックします。

2.  **.cpk** ファイル (WLK テスト結果) を参照し、 **[Load]** (読み込み) をクリックします。

3.  デバイスがインボックスではない場合は、ドライバー、ロケール、シンボルを追加するよう求められます (シンボルは省略可)。

4.  テスト結果が追加されたら、 **[Add DTM Results]** (DTM 結果の追加) ダイアログ ボックスを閉じて、情報をメイン画面に追加します。

5.  追加されたエントリを編集するには、 **[Edit]** (編集) ボタンをクリックします。 すべての情報が入力された状態で **[Edit DTM Results]** (DTM 結果の編集) ダイアログ ボックスが表示されます。

6.  すべてのエントリを追加した後で、 **[Create Package]** (パッケージの作成) ボタンをクリックして提出パッケージを作成できます。

7.  パッケージの作成中にエラーを検出することができます。 エラーが検出されると、パッケージの作成は中止されます。 エラーが検出されたエントリは、赤色で強調表示されます。 エラーをもう一度表示するには、メイン ウィンドウの **[View Errors]** (エラーの表示) ボタンをクリックします。 パッケージを作成するには、すべてのエラーが修正されている必要があります。 エラーを修正するには、エントリを編集し、ドライバーまたはテスト結果を更新します。

8.  すべてのエラーを修正した後、提出パッケージを作成できます。 提出パッケージは、 **.xml** ファイルと同じ名前で同じ場所に作成されます。

 

 





