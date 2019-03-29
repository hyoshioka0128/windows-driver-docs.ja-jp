---
title: ドライバーの署名のインストールのトラブルシューティング
description: リリースで署名されたドライバーをインストールすると、インストール、アンインストール、およびが説明されている 4 つのメソッドのいずれかを使用してをインストールするときに必要な追加の手順を 2 つを除くでテスト署名、Test-Signed ドライバー パッケージの読み込みで説明されていると同じです。
ms.assetid: 36624611-1FE6-4B88-B785-44D6A81F61FF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c65fdb85ef48cec5515b9f3029eeb42b1797e588
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350395"
---
# <a name="troubleshooting-driver-signing-installation"></a>ドライバーの署名のインストールのトラブルシューティング


説明されているものと同じリリースで署名されたドライバーのインストールは**インストール、アンインストール、および Test-Signed ドライバー パッケージを読み込む**で[テスト署名](test-signing.md)、ときに必要な追加の手順を 2 つを除く説明されている 4 つのメソッドのいずれかを使用してインストールします。 ハードウェアの追加ウィザードを使用して、リリースで署名されたドライバーをインストールするには、一般的なインストールの問題を含む 2 つの手順で追加は示しています。

1.  管理者特権でコマンド ウィンドウを開きます
2.  ハードウェアの追加ウィザードを起動し、2 番目のページに移動の横にあるをクリックする hdwwiz.cpl を実行します。
3.  高度なオプションを選択し、[次へ] をクリックします。
4.  選択は、リスト ボックスからすべてのデバイスを表示し、[次へ] をクリックします
5.  ディスク オプションを選択します。
6.  パスを含む、c: フォルダーを入力します\\トースター ドライバー パッケージ
7.  Inf ファイルを選択し、[開く] をクリックしてください
8.  [OK] をクリックします。
9.  次の 2 つのページで [次へ]、インストールを完了するには、[完了] をクリックし、
10. 「このデバイスのソフトウェアをインストールしてもよろしいですか? は」を確認するダイアログ ボックスでインストール をクリックします。
11. [完了] をクリックして、インストールを完了します。

手順 10 では、次の Windows セキュリティ ダイアログ ボックスを表示します。

![windows セキュリティ ダイアログ ボックスを示すスクリーン ショット](images/tutorialwindowssecurityinstalldialog.png)

チェック ボックスをオンには表示されませんこのダイアログ ボックスもう一度、コンピューターでドライバーがもう一度インストールされている場合、ドライバーが何らかの理由で削除されるかどうか。

**注**  パブリッシャー情報が正確である、カタログの署名に使用された SPC に基づいてシステムを確認します。 発行者の信頼レベルが不明の場合: Contoso.com—the システム ダイアログ ボックスを表示するには、true とになります。 インストールを続行するには、ユーザーはインストールをクリックする必要があります。 信頼とドライバーのインストールの詳細については、次を参照してください。[コード署名のベスト プラクティス](https://msdn.microsoft.com/library/windows/hardware/dn653556)します。

 

未署名のドライバは一方が x64 では機能しない未署名のドライバをインストールするユーザーは、次のダイアログ ボックスを表示、Windows のバージョン。

![windows セキュリティの警告ダイアログを示すスクリーン ショット](images/tutorialwindowssecurityinstallwarning.png)

## <a name="verify-that-the-release-signed-driver-is-operating-correctly"></a>Release-Signed ドライバーが正しく動作であることを確認します。


デバイス マネージャーを使用して、テスト署名されたドライバーに対して前に説明したように、ドライバーのプロパティを表示します。 以下は、画面は、ドライバーが動作しているかを表示します。

![デバイス マネージャにトースター デバイスを示すスクリーン ショット](images/tutorialtoasterpackageindevicemgr.png)

## <a name="troubleshoot-release-signed-drivers"></a>リリース署名されたドライバーをトラブルシューティングします。


次の一覧は、署名の読み込みに関する問題のトラブルシューティングまたは署名されたドライバーをテストするいくつかの一般的な方法を示しています。

-   」の説明に従って、ドライバーが読み込まれ、署名されているかどうかを確認するハードウェアの追加ウィザードまたはデバイス マネージャーを使用して**いることを確認、Test-Signed ドライバーが動作して正しく**の[テスト署名](test-signing.md)します。
-   Windows で作成した setupapi.dev.log ファイルを開く\\inf ディレクトリ ドライバーをインストール後します。 レジストリ エントリを設定して、ドライバーをインストールする前に setupapi.dev.log ファイルの名前の変更に関するセクションを参照してください。
-   Windows セキュリティの監査ログとコードの整合性イベント ログを確認します。

## <a name="analyzing-the-setupapidevlog-file"></a>Setupapi.dev.log ファイルの分析


前述の前に、ドライバーのインストール情報ログに記録されます (付加)、Windows で setupapi.dev.log ファイル\\inf ディレクトリ。 ドライバーをインストールする前にファイルの名前変更は、新しいログ ファイルが生成されます。 新しいログ ファイルは、新しいドライバーのインストールの重要なログを検索しやすくなります。 ログ ファイルは、メモ帳で開きます。

最初の列を左に 1 つの感嘆符を必要があります"!" 複数の感嘆符、または"!!!"です。 1 つのマークは、警告メッセージの種類が、3 つの感嘆符はエラーを示す値になります。

提供された SPC 証明書を次 1 つの感嘆符 CA ベンダーで署名されたドライバー パッケージのリリースをインストールするときに表示されます。 これらは、単なる警告を示すこと、cat ファイルがまだ検証されていません。

```cpp
!    sig:                Verifying file against specific (valid) catalog failed! (0x800b0109)
!    sig:                Error 0x800b0109: A certificate chain processed, but terminated in a root certificate which is not trusted by the trust provider.
     sig:                Success: File is signed in Authenticode(tm) catalog.
     sig:                Error 0xe0000242: The publisher of an Authenticode(tm) signed catalog has not yet been established as trusted.
```

ドライバーのインストールの手順 10. を参照してくださいし、[インストール] ボタンをクリックして、表示は、ほとんどの場合は、その後、ドライバーはインストールして読み込む問題なくログの下。 デバイス マネージャーは、すべてのエラーまたはドライバーの黄色の感嘆符は報告されません。

```cpp
!    sto:           Driver package signer is unknown but user trusts the signer.
```

上記の時点までの作業に関係なく、ドライバーが読み込まれない場合は、次のエラーも表示ログ ファイルに記録します。

Setupapi.dev.log ファイルは、次のエラーを報告もいます。

```cpp
!!!  dvi:                          Device not started: Device has problem: 0x34: CM_PROB_UNSIGNED_DRIVER.
```

0x34 がコード 52 であることに注意してください。

この時点で、ログ ファイルに戻りを任意の感嘆符のドライバー バイナリが通知されたかどうかの検索を試行する可能性があります。 いくつかを示す手掛かりを提供することがあります。 でもそれ以外の場合、説明されている「signtool 確認」コマンドを実行する必要があります前に、cat ファイルとその他の埋め込み署名済みバイナリのドライバーの署名に問題がないことを確認します。

ほとんどのログ ファイルの情報は、問題を解決するのには十分です。 根本原因を見つけるには上記のチェックに失敗した場合次のアプローチは、Windows セキュリティ監査ログとコードの整合性イベント ログを確認するこれは、次のセクションで説明します。

Setupapi.dev.log ファイルでは、サービスのバイナリ ファイルとしてコピーはコミットされていないが、サービスを開始しようとする OS ドライバー サービスが開始に失敗したことが見つかった場合に備えて、ドライバー ファイルのコピーとコミット時間の情報を追跡できます。 再起動が正常にサービスを開始します。 ログ ファイルに次の操作のシーケンスを参照してください。

```cpp
>>>  Section start 2014/02/08 14:54:56.463
```

後で 次へ:

```cpp
!    inf:                     Could not start service 'toaster'.
```

ファイルのコピー操作があります。

```cpp
<snip>
flq:                {FILE_QUEUE_COPY}
     flq:                     CopyStyle      - 0x00000000
     flq:                     SourceRootPath - 'C:\Windows\System32\DriverStore\FileRepository\Toaster.inf_amd64_d9b35403a0fe4391\'
     flq:                     SourceFilename - 'toaster.exe'
     flq:                     TargetDirectory- 'C:\Windows\System32\drivers'
     flq:                     TargetFilename - 'toaster.exe'
```

ファイルが次にコミットします。 開始時刻と終了時刻を比較します。

```cpp
flq:           {_commit_file_queue} 14:54:56.711
<snip>
     flq:                     {_commit_copyfile}
     flq:                          Copying 'C:\Windows\System32\DriverStore\FileRepository\Toaster.inf_amd64_d9b35403a0fe4391\o2flash.exe' to 'C:\Windows\System32\drivers\o2flash.exe'.
     flq:                          CopyFile: 'C:\Windows\System32\DriverStore\FileRepository\Toaster.inf_amd64_d9b35403a0fe4391\o2flash.exe' to 'C:\Windows\System32\drivers\SETDA81.tmp'
     flq:                          MoveFile: 'C:\Windows\System32\drivers\SETDA81.tmp' to 'C:\Windows\System32\drivers\toaster.exe'
     cpy:                          Applied 'OEM Legacy' protection on file 'C:\Windows\System32\drivers\toaster.exe'.
     flq:                          Caller applied security to file 'C:\Windows\System32\drivers\toaster.exe'.
     flq:                     {_commit_copyfile exit OK}
<snip>
     sto:      {Configure Driver Package: exit(0x00000bc3)}
     ndv:      Restart required for any devices using this driver.
<snip>
<<<  Section end 2014/02/08 14:54:57.024
<<<  [Exit status: SUCCESS]
```

上記は、Windows 7 で正しく動作しますが、Windows 8.0 および 8.1、バグの検出に至ったで失敗しましたが、ドライバーの更新のケースでした。

## <a name="using-the-windows-security-audit-log"></a>Windows セキュリティの監査ログの使用


ドライバーが有効な署名が欠落しているため、読み込みに失敗した場合、失敗の監査イベントは、コードの整合性が、ドライバー ファイルの画像のハッシュを確認できませんでしたを示す Windows セキュリティ ログに記録されます。 ログ エントリには、ドライバー ファイルの完全なパス名が含まれます。 監査のローカル セキュリティ ポリシーにより、システム障害イベントのログ記録する場合にのみ、セキュリティ ログの監査イベントが生成されます。

**注**  セキュリティの監査ログを明示的に有効にする必要があります。 詳細については、次を参照してください。[付録 3。コードの整合性イベント ログとシステムの監査を有効にする](appendix-3--enable-code-integrity-event-logging-and-system-auditing.md)します。

 

セキュリティ ログを確認します。

1.  管理者特権のコマンド ウィンドウを開きます。
2.  Windows イベント ビューアーを起動するには、Eventvwr.exe を実行します。 イベント ビューアーは、コントロール パネルのコンピューターの管理アプリケーションから起動することもできます。
3.  Windows セキュリティの監査ログを開きます。
4.  イベント id は 5038 システム整合性のイベント ログを確認します。
5.  イベントの詳細な説明を提供します。 そのイベントのプロパティ ダイアログ ボックスを表示するログ エントリをダブルクリックします。

以下のスクリーン ショットは、符号なしの Toaster.sys ファイルが原因で、セキュリティ監査ログ イベントのイベントのプロパティ ダイアログ ボックスを示しています。

![showig イベントの [プロパティ] ダイアログ ボックスのスクリーン ショット](images/tutorialeventprops.png)

## <a name="using-the-code-integrity-event-operational-event-log"></a>コードの整合性イベント操作イベント ログを使用します。


ドライバーが署名されていないか、イメージの検証エラーが発生したため、読み込みに失敗した場合、コードの整合性は、コードの整合性の操作イベント ログで、イベントを記録します。 コードの整合性の操作イベントが常に有効にします。

コードの整合性イベントは、イベント ビューアーで表示できます。

## <a name="to-examine-the-code-integrity-operational-log"></a>コードの整合性の操作ログを確認するには


1.  管理者特権のコマンド ウィンドウを開きます。
2.  Windows イベント ビューアーを起動するには、Eventvwr.exe を実行します。 イベント ビューアーは、コンピュータの管理コントロール パネル アプリケーションからも開始できます。
3.  Windows コードの整合性のログを開きます。
4.  イベントの詳細な説明を提供します。 そのイベントのプロパティ ダイアログ ボックスを表示するログ エントリをダブルクリックします。

以下のスクリーン ショットは、符号なしの Toaster.sys ファイルによって発生したコードの整合性の操作ログ イベントのイベントのプロパティ ダイアログ ボックスを示しています。

![イベント ビューアーを示すスクリーン ショット](images/tutorialeventvwr.png)

## <a name="using-the-informational-events-in-the-code-integrity-verbose-log"></a>コードの整合性の詳細ログに情報イベントを使用します。


コードの整合性と情報ログの詳細ビューでは、カーネル モード イメージの検証チェックをすべてのイベントを追跡します。 これらのイベントは、システムに読み込まれるすべてのドライバーの検証を成功のイメージを表示します。

コードの整合性の詳細なビューを有効にします。

1.  前の例のように、イベント ビューアーを起動します。
2.  フォーカスを設定するコードの整合性のノードをクリックします。
3.  コードの整合性を右クリックし、ショートカット メニューから表示項目を選択します。
4.  分析の表示 を選択して、デバッグ ログ。 2 つの追加ノードのサブツリーが作成されます。運用と詳細。
5.  詳細なノードを右クリックし、ショートカット メニューからプロパティを選択します。
6.  [全般] タブには、詳細ログ モードを有効にするログ記録を有効にするを選択します。
7.  すべてのカーネル モード バイナリを再読み込みするシステムを再起動します。
8.  再起動後、コンピューターの管理の MMC スナップインを開くし、コードの整合性の詳細なイベント ログを表示します。

その他の既知のドライバー署名問題のいくつかが記載されて[付録 4。ドライバーの問題を署名](appendix-4--driver-signing-issues.md)します。

 

 





