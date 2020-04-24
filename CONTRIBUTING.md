# <a name="contributing-to-windows-driver-documentation"></a>Windows ドライバー ドキュメントへの投稿

このページでは、Windows ドライバー ドキュメントへの投稿の基本的な手順について説明します。

変更を提案する方法を紹介した[入門ビデオ](https://channel9.msdn.com/Blogs/WinHEC/Contributing-to-MSDN-and-TechNet-Documentation)もご覧ください。

## <a name="sign-a-cla"></a>CLA に署名する

Microsoft の従業員以外の方が複数行にわたる変更を投稿する場合は、[Microsoft Contribution Licensing Agreement (CLA) に署名する](https://cla.microsoft.com/)必要があります。 

Microsoft の従業員の場合は、必ず [GitHub アカウントとエイリアスをリンク](https://opensource.microsoft.com/link)してください。

以前に Microsoft リポジトリに投稿したことがある場合、 この手順は既に完了しています。


## <a name="proposing-a-change"></a>変更を提案する

ドキュメントへの変更を提案する場合は、次の手順に従います。

1. Docs.microsoft.com のページを表示している場合は、ページの右上にある **[編集]** ボタンをクリックします。  [GitHub リポジトリ](https://github.com/MicrosoftDocs/windows-driver-docs)内の対応するマークダウン ソース ファイルにリダイレクトされます。  既に [GitHub リポジトリ](https://github.com/MicrosoftDocs/windows-driver-docs)を表示している場合は、変更したいソース ファイルに移動するだけです。
2. GitHub アカウントがまだない場合は、右上の **[サインアップ]** をクリックして新しいアカウントを作成します。
3. 変更したい GitHub ページで、鉛筆アイコンをクリックします。
4. ファイルを変更し、[Preview] タブを使って変更内容に問題がないことを確認します。
5. 完了したら、変更をコミットし、プル要求を開きます。

プル要求が作成されると、Windows ドライバー ドキュメント チームのメンバーによって変更内容が確認されます。 

要求が受理された場合、更新が https://docs.microsoft.com/windows-hardware/drivers に公開されます。

Microsoft の従業員がプライベート環境で共同作業する必要がある場合は、windowsdriverdev エイリアスに問い合わせてください。

## <a name="making-more-substantial-changes"></a>さらに大幅な変更を加える

既存の記事に大幅な変更を加える場合、画像を追加または変更する場合、または新しい記事を投稿する場合は、公式リポジトリを自分の GitHub アカウントに分岐し、ローカルの複製を作成することをお勧めします。

詳しくは、[リポジトリの分岐](https://help.github.com/articles/fork-a-repo/)に関する記事をご覧ください。

## <a name="using-issues-to-provide-feedback-on-windows-driver-documentation"></a>問題を使用して Windows ドライバー ドキュメントへのフィードバックを提供する

ドキュメントについて変更を提案するのではなく、フィードバックを提供したい場合は、[問題を作成](https://github.com/MicrosoftDocs/windows-driver-docs/issues)します。

必ずトピックのタイトルとページの URL を含めてください。

## <a name="resources"></a>参照情報

Markdown の編集には、使い慣れたテキスト エディターを使用できます。  Microsoft の無料の軽量オープン ソース エディター、[Visual Studio Code](https://code.visualstudio.com/) をお勧めします。

マークダウンの基本事項はほんの数分で学習できます。  最初に、[マークダウンの概要に関するページ](https://guides.github.com/features/mastering-markdown/)をご覧ください。
