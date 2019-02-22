---
title: ファイル共有 (SMB) のシンボル サーバー
description: 単にファイル共有を作成して、そのファイル共有へのアクセスをユーザーに許可するは、SMB シンボル サーバーを実行します。
ms.assetid: C5CF9665-9289-48EB-AA12-8881F812488A
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2bbaeed3a565e8854074439b410d2cc17494fff
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556539"
---
# <a name="file-share-smb-symbol-server"></a>ファイル共有 (SMB) のシンボル サーバー


単にファイル共有を作成して、そのファイル共有へのアクセスをユーザーに許可するは、SMB シンボル サーバーを実行します。

## <a name="span-idcreatingasmbfilesharesymbolstorespanspan-idcreatingasmbfilesharesymbolstorespanspan-idcreatingasmbfilesharesymbolstorespancreating-a-smb-file-share-symbol-store"></a><span id="Creating_a_SMB_File_Share_Symbol_Store_"></span><span id="creating_a_smb_file_share_symbol_store_"></span><span id="CREATING_A_SMB_FILE_SHARE_SYMBOL_STORE_"></span>SMB ファイル共有のシンボル ストアを作成します。


ファイル共有を作成してセキュリティを割り当てるには、Windows エクスプ ローラーまたはコンピュータの管理を使用します。 これらの手順は、シンボルに配置されることを想定しています*d:\\SymStore\\シンボル*します。 Windows エクスプ ローラーを使用してこれらの手順を完了するには。

1. 開いている**Windows エクスプ ローラー**します。

2. 右クリックして*d:\\SymStore\\シンボル*選択**プロパティ**します。

3. をクリックして、**共有**タブ。

4. をクリックして**詳細な共有**. .

5. 確認*このフォルダーを共有*します。

6. をクリックして**権限**します。

7. 削除、 *Everyone*グループ。

8. 使用して**を追加しています.** アクセスを必要とするユーザー/セキュリティ グループを追加します。

9. 追加の各ユーザーまたはセキュリティ グループの読み取りまたは読み取りと変更のアクセスを付与します。

10. をクリックして**OK** (アクセス許可ダイアログ)。

11. をクリックして**OK** ([詳細な共有] ダイアログ)。

12. キーを押して**閉じる**([プロパティ] ダイアログ)。

コンピューターの管理を使用してこれらの手順を完了するには。

1. 型*コンピューター*ウィンドウを起動します (Windows 8 PC として解決) にします。

2. 右クリックして*管理*します。

3. 移動します*システム ツール |共有フォルダーの |共有*します。

4. 右クリックして**新規 |共有。** .

5. キーを押して**次**(共有フォルダー ウィザード ダイアログの作成) します。

6. 入力**d:\\SymStore\\シンボル**としてフォルダーのパス。

7. キーを押して**次**2 回クリックします。

8. 選択**アクセス許可のカスタマイズ**します。

9. キーを押して**カスタム.** .

10. 削除*Everyone*します。

11. 使用して**を追加しています.** アクセスを必要とするユーザー/セキュリティ グループを追加します。

12. 追加の各ユーザーまたはセキュリティ グループの読み取りまたは読み取りと変更のアクセスを付与します。

13. キーを押して**OK** (アクセス許可のカスタマイズ ダイアログ)。

14. キーを押して**完了**プロセスを完了するには、2 回クリックします。

## <a name="span-idtestthesmbfilesharespanspan-idtestthesmbfilesharespanspan-idtestthesmbfilesharespantest-the-smb-file-share"></a><span id="Test_The_SMB_File_Share"></span><span id="test_the_smb_file_share"></span><span id="TEST_THE_SMB_FILE_SHARE"></span>SMB ファイル共有をテストします。


このシンボル パスを使用するデバッガーを構成します。

```text
srv*C:\Symbols*\\MachineName\Symbols
```

デバッガーで参照されている Pdb の場所を表示するには、lm (モジュールの一覧) のコマンドを使用します。 C: での Pdb へのパスが始まります\\シンボル。 実行して"! sym ノイズの多い"、".reload/f"記号とからのイメージのダウンロードのシンボルの広範なログ記録をわかり、 \\ \\MachineName\\c: シンボル ファイル サーバー\\シンボル。

## <a name="span-idfilesharesymbolpathspanspan-idfilesharesymbolpathspanspan-idfilesharesymbolpathspanfile-share-symbol-path"></a><span id="File_Share_Symbol_Path"></span><span id="file_share_symbol_path"></span><span id="FILE_SHARE_SYMBOL_PATH"></span>ファイル共有のシンボル パス


ファイル共有を使用するデバッガーのシンボル パス (.sympath) を構成する複数の方法はあります。 シンボル パスの構文は、シンボル ファイルがキャッシュ可能か、ローカルと、キャッシュされているかどうかを決定します。

ファイル共有の使用 (ローカル キャッシュなし) に指示します。

```text
srv*\\MachineName\Symbols
```

特定のローカル フォルダーにファイル共有のファイルのローカル キャッシュ (例: c:\\シンボル)。

```text
srv*c:\Symbols*\\MachineName\Symbols
```

%Dbghelp するファイル共有のファイルのローカル キャッシュ\_HOMEDIR %\\Sym フォルダー。

```text
srv**\\MachineName\Symbols
```

2 番目の"\*"前述の例では、既定のサーバーのローカル キャッシュを表します。

場合、DBGHELP\_HOMEDIR 変数が設定されていない DBGHELP\_HOMEDIR 既定値は、デバッガーの実行可能フォルダー (たとえば c:\\Program Files\\Windows キット\\10.0\\デバッガー\\x86) と、c: で発生するキャッシュ\\Program Files\\Windows キット\\10.0\\デバッガー\\x86\\.sym となります

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[シンボル ストアのフォルダー ツリー](symbol-store-folder-tree.md)

 

 






