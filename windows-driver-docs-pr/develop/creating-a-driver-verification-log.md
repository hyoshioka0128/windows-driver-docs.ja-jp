---
ms.assetid: 5EB802D0-1894-4D64-ACB0-77B848B7E644
title: ドライバー検証ツール ログの作成
description: Windows Server 2012 ハードウェア認定プログラムでは、該当するドライバーを提出するときに、ドライバー検証ツール ログ (DVL) を含める必要があります。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8199e7671bc8cfc1790f3ba8ea59962f747d3967
ms.sourcegitcommit: fac288eb2cceb6a7a8248ae0f8086553d1659b23
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2019
ms.locfileid: "56588959"
---
# <a name="creating-a-driver-verification-log"></a>ドライバー検証ツール ログの作成

Windows Server [ハードウェア認定プログラム](https://docs.microsoft.com/en-us/windows-hardware/design/compatibility/)では、すべてのドライバーを提出するときに、ドライバー検証ツール ログ (DVL) を含める必要があります。 DVL には、コード分析 (CA) と静的ドライバー検証ツール (SDV) のログ ファイルからの結果の要約が含まれています。 DVL には、ソースの情報は含まれていません。 ドライバーの DVL を作成する前に、コード分析ツールと静的ドライバー検証ツールを実行する必要があります。

**ドライバー検証ツール ログを作成するには**

1.  コード分析ツールを実行する前に、最新の Windows Driver Kit (WDK) を使ってドライバーのビルドとリンクができることを確認します。
2.  ドライバー ソリューションでは、ソリューション構成としてリリース構成、ソリューション プラットフォームとして x64 が選択されていることを確認します。
3.  [静的ドライバー検証ツール](https://msdn.microsoft.com/Library/Windows/Hardware/Ff552808)を実行します。 ログ ファイルの作成方法については、「[静的ドライバー検証ツールのログ ファイルの作成](creating-a-log-file-for-static-driver-verifier.md)」と「[ドライバーの不具合を見つけるための静的ドライバー検証ツールの使用](https://msdn.microsoft.com/Library/Windows/Hardware/Hh454281)」をご覧ください。
4.  ドライバーのコード分析ツールを実行します。 見つかった欠陥に対処し、修正します。 「[コード分析ツールのログ ファイルの作成](creating-a-log-file-for-the-code-analysis-tool.md)」と「[ドライバーのコード分析を実行する方法](https://msdn.microsoft.com/Library/Windows/Hardware/Hh454219)」をご覧ください。 コード分析について詳しくは、[コード分析による C/C++ コード品質の分析に関するページ](https://go.microsoft.com/fwlink/p/?linkid=226836)をご覧ください。
5.  ドライバーの検証ツール ログを作成します。 **[ドライバー]** メニューの **[Create Driver Verification Log]** (ドライバーの検証ツール ログの作成) をクリックします。
6.  コード分析ログと静的ドライバー検証ツール ログの両方のファイルが検出されていることを確認します。 **[作成]** をクリックします。

ドライバー検証ツール ログのファイル名拡張子は、.DVL.XML です。 ログは、プロジェクト フォルダーに作成されます (例: \\*myDriverProject*\\*myDriverName*.DVL.XML)。

**注**  SDV ではドライバーのクリーン リビルドが実行されます。これにより、コード分析ログが削除されます。  そのため、CA を実行する前に SDV を実行してください。

**注**  [Windows ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?linkid=254893) を使ってドライバーをテストする準備ができたら、ドライバー検証ツール ログをテスト コンピューターの %systemdrive%\\DVL ディレクトリにコピーする必要があります。 新しいドライバー検証ツール ログをコピーする前に、テスト コンピューターのこのディレクトリの内容を必ず削除してください。

 

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


コード分析ツール、静的ドライバー検証ツール、ドライバーの検証ツール ログに関する最新情報については、WDK リリース ノートをご覧ください。 リリース ノートは、[Windows Driver Kit (WDK) のダウンロード ページ](https://go.microsoft.com/fwlink/p/?linkid=254897)で入手できます。

**重要**   DVL ファイルでタイムアウト、領域不足などの失敗した結果があっても、認定用に申請できます。 これにより、HCK の静的ツール テストに不合格になることはありません。 HCK 2.0 では、Static Tools (静的ツール) テストに必要なのは、コード分析と SDV が実行されたことを示す DVL ファイルだけです。必ずしもすべてのルールに合格する必要はありません。

 

Visual Studio コマンド プロンプト ウィンドウから、Visual Studio と共にインストールされた Visual Studio Native Tools コマンド プロンプトまたは Enterprise Windows Driver Kit (EWDK) のどちらかを使用してドライバー検証ツール ログを作成することもできます。

```cpp
msbuild.exe <vcxprojectfile> /target:dvl /p:Configuration="Release" /P:Platform=x64
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


* [静的ドライバー検証ツールのログ ファイルの作成](creating-a-log-file-for-static-driver-verifier.md)
* [コード分析ツールのログ ファイルの作成](creating-a-log-file-for-the-code-analysis-tool.md)
* [ハードウェア認定プログラム](https://go.microsoft.com/fwlink/p/?linkid=227016)
* [コード分析ツールによるドライバー品質の分析](analyzing-driver-quality-by-using-code-analysis-tools.md)
* [ドライバーのコード分析を実行する方法](https://msdn.microsoft.com/Library/Windows/Hardware/Hh454219)
* [ドライバーの不具合を見つけるための静的ドライバー検証ツールの使用](https://msdn.microsoft.com/Library/Windows/Hardware/Hh454281)
 

 






