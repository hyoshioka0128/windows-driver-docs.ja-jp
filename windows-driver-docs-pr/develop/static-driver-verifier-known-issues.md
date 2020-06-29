---
title: 静的ドライバー検証ツールの既知の問題
description: ''
author: selerner
ms.author: selerner
ms.date: 11/07/2018
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: 0a2ce71a213655ec65de73923052fd7f25424999
ms.sourcegitcommit: 444e055daa9b28e9fd9dc92dd0a3f1e62e215b31
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/10/2020
ms.locfileid: "84666164"
---
# <a name="static-driver-verifier-known-issues---windows-10-version-1809"></a>静的ドライバー検証ツールの既知の問題 - Windows 10 バージョン 1809

このページでは、Windows Driver Kit (WDK) で静的ドライバー検証 (SDV) ツールを使うと発生する可能性がある一般的な問題について説明します。 以下の情報は、Windows 10 October 2018 Update (バージョン 1809) に付属するバージョンのツールに特に関係のあるものです。

最新の公式 WDK に関する既知の SDV の問題については、[WDK の既知の問題](https://social.msdn.microsoft.com/Forums/en-US/96c770a9-19a3-42d0-8d0e-bd200285d980/hardware-development-kits-for-windows-10-version-2004?forum=wdk)に関する記事を参照してください。

## <a name="interceptedbuild-failures"></a>InterceptedBuild エラー

主な現象:SDV が `FATAL ERROR: Unrecoverable error in InterceptedBuild stage` で失敗します。  

DVL ファイルを調べるときは、`ScoreName="[driverName].[architecture].SDV.NA.Reason"` および `ScoreUnit="Unrecoverable error in InterceptedBuild stage."` で `AssessmentScore` の値を確認します

InterceptedBuild エラーでは、以下の手順を実行して問題を診断します。

1. Visual Studio 2017 のネイティブ ツール コマンド ラインから、/debug フラグを指定して SDV を再実行します。  コマンドのオプションについて詳しくは、「[Static Driver Verifier commands (静的ドライバー検証ツールのコマンド)](https://docs.microsoft.com/windows-hardware/drivers/devtest/-static-driver-verifier-commands--msbuild-)」をご覧ください。

    a。 最初に、依存しているライブラリ プロジェクトで SDV のライブラリ関数を実行します。  たとえば、 `msbuild /p:Configuration=Release /p:Platform=x64 /t:sdv /p:inputs="/lib /debug"`と指定します。

    b. 次に、ドライバー プロジェクト自体で SDV を実行します。  たとえば次のようになります。`msbuild /p:Configuration=Release /p:Platform=x64 /t:sdv /p:inputs="/check /debug"`

2. InterceptedBuild ステージでエラーが再度発生することを確認します。

3. SDV を実行するときは、ドライバー フォルダーに生成された `sdv` フォルダーに移動します。

4. `smvcl.log` を開き、"内部コンパイラ エラー" という語句を探します。

    a。 "**内部コンパイラ エラー**" および "**致命的なエラー C1001: コンパイラで内部エラーが発生しました。 (コンパイラ ファイル 'msc1.cpp'、行 1511)** " のような語句が含まれるエラー メッセージが存在する場合、これは Errata (Errata ID 40705) が必要な既知の問題です。 さらにサポートが必要な場合は、<stlogohelp@microsoft.com> にメールでご連絡ください。

    b. "**内部コンパイラ エラー**" が含まれるエラー メッセージは存在しても、上記のような内容ではない場合は、おそらく Errata は必要ですが、既存の既知の問題ではない可能性があります。  <stlogohelp@microsoft.com> にメールでご連絡ください。

    c. "**内部コンパイラ エラー**" が含まれる行がない場合は、"**エラー**" で始まる任意の行を探します。  Errata が必要な問題が存在するかどうかはわかりません。  <stlogohelp@microsoft.com> にメールでご連絡ください。

5. smvlink1.log を開き、"**内部コンパイラ エラー**" という語句を探します。

    a。 "**内部コンパイラ エラー**" および "**slamcl: error: at phase 2: out of memory (slamcl: エラー: フェーズ 2: メモリ不足)** " が含まれるエラー メッセージが存在する場合、これは Errata が必要な既知の問題です。

    b. "**内部コンパイラ エラー**" が含まれる行がない場合は、"**エラー**" で始まる任意の行を探します。  Errata が必要な問題が存在するかどうかはわかりません。  <stlogohelp@microsoft.com> にメールでご連絡ください。

    c. 上記のいずれにも該当しない場合は、MSFT にサポートを依頼します。

MSFT にサポートを依頼するには、以下を実行してソース コードが共有されていないことを確認してください。

1. /debug フラグを有効にして SDV を実行し、出力をテキスト ファイルにパイプします。

2. ドライバー ディレクトリの `sdv` フォルダーに移動し、次のコマンドを実行して、ソースが公開されている可能性のあるビルド結果をクリアします。

    ```cmd
    del /s *.obj
    del /s *.rawcfg*
    del /s *.li
    del /s *.pdb
    del /s *.sys
    ```

3. 次のファイルを <stlogohelp@microsoft.com> に送信します。

    a。 SDV を実行した出力が含まれるテキスト ファイル

    b. **smexecute-NormalBuild.log** ファイル

    c. **smvexecute-InterceptedBuild.log** ファイル

    d. "sdv" サブフォルダー

## <a name="visual-studio-c-2013-runtimes-not-present"></a>Visual Studio C++ 2013 のランタイムが存在しない

主な現象:Visual Studio C++ 2012 および 2013 のランタイムがないシステムで SDV を実行すると、ポップアップ ボックスに次のようなエラーが表示される場合があります。"\[MSVCR110.dll または VCOMP110.dll\] が見つからないため、コードの実行を続行できません。  プログラムを再インストールすると、この問題が解決する可能性があります。"

このケースでの解決策は、X86 と x64 両方の Visual Studio 2012 および 2013 の Visual C++ 再頒布可能パッケージをインストールすることです。

## <a name="best-practice-use-visual-studio-2017-version-158"></a>ベスト プラクティス: Visual Studio 2017 バージョン 15.8 を使用します 

既定では、Visual Studio 15.7 でコード分析によってドライバーが自動的にビルドされることはありません。  生成されるバイナリにドライバーが依存している場合、 **[出力]** ウィンドウにエラーが表示される可能性があります。  代わりに、バージョン 15.8 を使うことをお勧めします。

## <a name="dvl-generation-failure-after-removing-configuration-from-a-project"></a>プロジェクトから構成を削除した後の DVL 生成失敗

主な現象:[構成マネージャー] ウィンドウでプロジェクトから構成を削除した後、 **[Create Driver Verification Log]\(ドライバー検証ツール ログの作成\)** を選択すると、次のメッセージを表示されます。`Please select a driver project. Driver Verification Log cannot be created for the selected platform tool set: 'v100'"`

対応策 : 

1. プロジェクト ファイルをバックアップした後、テキスト エディターでプロジェクト ファイルを開きます。

2. `\<PropertyGroup Label="Globals"\>` セクションで、2 つの XML タグを探します。1 つは `\<Configuration\>\[Configuration type\]\</Configuration\>` という形式で、もう 1 つは `\<Platform Condition="'$(Platform)' == ''"\>\[Architecture\]\</Platform\>` という形式です。ここで、`\[Configuration type\]` および `\[Architecture\]` は、この種類のプロジェクトの既定の構成とリリースです。

3. `\[Configuration type\]` および `\[Architecture\]` は自分のプロジェクトに適した値です。  たとえば、Win32 プラットフォームを削除した場合は、代わりに `\[Architecture\]` を x64 などに更新します。

別の回避策:

1. Visual Studio 2017 のネイティブ ツール コマンド プロンプトを開きます。

2. ドライバーのフォルダーに移動します。

3. `msbuild [Your Project] /p:Configuration=[Configuration type]  /p:Platform=[Architecture] /t:dvl` を実行します。ここで、`\[Your Project\]` は vcxproj ファイル、`\[Configuration type\]` は Release などの有効な構成、`\[Architecture\]` は x64 などの有効なアーキテクチャです。

## <a name="dvl-generation-does-not-work-on-servercore-use-server-gui"></a>ServerCore ではDVL 生成が動作しないので Server GUI を使用する

実行すると、静的ツールのロゴ テストが失敗します。  テスト ログを確認すると、次のようなエラーが発生しています。`Failed to load 'C:\hlk\JobsWorkingDir\Tasks\WTTJobRun4749E809-0166-E811-8368-F4521454FFE1\Devfund_DvlTest.dll'. (Could not load managed test module because RoMetadata.dll could not be found)`

TAEF パッケージが配置されていること、または RoMetadata.dll が PATH 環境変数内の場所に配置されていることを確認します。  

主要な現象としては、RoMetadata.dll の読み込みが失敗します。

インストールされている Server GUI のアーキテクチャおよび Windows バージョンが ServerCore のインストールと同じ場合は、Server GUI から ServerCore に RoMetadata.dll ファイルをコピーします。  DLL は System32 フォルダー (たとえば `C:\Windows\System32`) にあり、ServerCore マシン上の同じフォルダーに配置する必要があります。  これにより、ServerCore でテストを実行できるようになるはずです。  問題が引き続き発生する場合は、次の回避策を参照してください。

2 つ目の回避策は、Server GUI で実行してから、パッケージを、Server Core の結果が含まれるパッケージとマージします。 パッケージのマージについては、「[Merge packages](https://docs.microsoft.com/windows-hardware/test/hlk/user/merge-packages)」 (パッケージをマージする) をご覧ください。

## <a name="static-driver-verifier-fails-with-exiting-libexeiwrapexe-with-0xc0000142-error"></a>既存の lib.exe/iwrap.exe を使用すると静的ドライバー検証ツールが 0xc0000142 エラーで失敗する

smvbuild.log ファイルには、次のエラーのようなメッセージが書き込まれています。

```
c:\Program Files\Microsoft Visual Studio\2017\BuildTools\Common7\IDE\VC\VCTargets\Microsoft.CppCommon.targets(1144,5): error MSB6006: "Lib.exe" exited with code -1073741502.

Done executing task "LIB" -- FAILED.
```

これは既知の問題です。 この問題によって WHCP 認定がブロックされている場合は、Errata 41600 を使用してください。
