---
ms.assetid: 4985B206-9E7F-45FE-9067-7CFD15A7AAAD
title: コード分析ツールのログ ファイルの作成
description: Windows Server 2012 ハードウェア認定プログラムでは、該当するドライバーを申請するときに、ドライバー検証ツール ログ (DVL) を含める必要があります。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e21d7f99c4c8c27402e0624152e79c8151bc8df
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "67370791"
---
# <a name="creating-a-log-file-for-the-code-analysis-tool"></a>コード分析ツールのログ ファイルの作成

Windows Server 2012 [ハードウェア認定プログラム](https://go.microsoft.com/fwlink/p/?linkid=227016)では、該当するドライバーを申請するときに、ドライバー検証ツール ログ (DVL) を含める必要があります。 ドライバーの DVL を作成する前に、コード分析ツールを実行する必要があります。 DVL には、コード分析と静的ドライバー検証ツールのログ ファイルからの結果の要約が含まれています。 ログ ファイルには、ソース コードの情報は含まれていません。

**ドライバーのコード分析を実行するには**

1.  Microsoft Visual Studio Ultimate 2012 でドライバー プロジェクト ファイルを選び、右クリックしてプロジェクトのプロパティを開きます。 **[構成]** として **[Windows 8 Release]\(Windows 8 リリース\)** を選び、 **[プラットフォーム]** として **[x64]** を選びます。
2.  **[分析]** メニューまたは **[ビルド]** メニューの **[ソリューションでコード分析を実行]** をクリックします。
3.  エラーや警告が見つかったら、 **[コード分析レポート]** ウィンドウを使ってエラーの原因を調べます。 警告メッセージは、これらの問題を修正するために利用します。 コード分析ツールについて詳しくは、「[ドライバーのコード分析を実行する方法](https://docs.microsoft.com/windows-hardware/drivers/devtest/how-to-run-code-analysis-for-drivers)」と[コード分析による C/C++ コード品質の分析に関するページ](https://go.microsoft.com/fwlink/p/?linkid=226836)をご覧ください。

ドライバーのコード分析ツールでは、ビルド構成およびプロジェクトのプラットフォームのサブディレクトリ (たとえば \\Windows 8Release\\x64) の vc.nativecodeanalysis.all.xml ファイルに結果が書き込まれます。

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


ドライバーのコード分析は、C/C++ プログラムの基本的なコーディング エラーをコンパイル時に検出する静的検証ツールです。(主に) カーネル モード ドライバーのコードからエラーを検出することを目的に特化されたモジュールが備わっています。 以前のバージョンの WDK では、コード分析用のドライバー固有のモジュールが、PREfast for Drivers (PFD) と呼ばれるスタンドアロン ツールに組み込まれていました。

コード分析ツールは、Visual Studio のコマンド プロンプト ウィンドウから実行することもできます。 以下のいずれかのバッチ ファイルを実行して、環境を設定します。

```cpp
"C:\Program Files\Microsoft Visual Studio 11.0\VC\vcvarsall.bat" x64
```

-または-

```cpp
"C:\Program Files (x86)\Microsoft Visual Studio 11.0\VC\vcvarsall.bat" x64
```

コード分析ツールを実行します。

```cpp
msbuild.exe <vcxprojectfile> /p:Configuration="Win8 Release" /P:Platform=x64 /target:clean
msbuild.exe <vcxprojectfile> /p:Configuration="Win8 Release" /P:Platform=x64 /P:RunCodeAnalysisOnce=True
```

ドライバーの検証ツール ログの要件に関する最新情報については、WDK リリース ノートをご覧ください。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


* [ドライバー検証ツール ログの作成](creating-a-driver-verification-log.md)
* [静的ドライバー検証ツールのログ ファイルの作成](creating-a-log-file-for-static-driver-verifier.md)
* [ドライバーのコード分析](https://docs.microsoft.com/windows-hardware/drivers/devtest/code-analysis-for-drivers)
* [ハードウェア認定プログラム](https://go.microsoft.com/fwlink/p/?linkid=227016)
* [コード分析による C/C++ コード品質の分析](https://go.microsoft.com/fwlink/p/?linkid=226836)
* [ドライバーのコード分析を実行する方法](https://docs.microsoft.com/windows-hardware/drivers/devtest/how-to-run-code-analysis-for-drivers)
 

 






