---
ms.assetid: EDA6357A-D18D-439D-A0DD-050BA51E1A79
title: 静的ドライバー検証ツールのログ ファイルの作成
description: Windows Server 2012 ハードウェア認定プログラムでは、該当するドライバーを申請するときに、ドライバー検証ツール ログ (DVL) を含める必要があります。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aeaca1ed749c665de3e43f981df4426860212254
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370796"
---
# <a name="creating-a-log-file-for-static-driver-verifier"></a>静的ドライバー検証ツールのログ ファイルの作成

Windows Server 2012 [ハードウェア認定プログラム](https://go.microsoft.com/fwlink/p/?linkid=227016)では、該当するドライバーを申請するときに、ドライバー検証ツール ログ (DVL) を含める必要があります。 ドライバーの DVL を作成する前に、[静的ドライバー検証ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier) (SDV) を実行する必要があります。 DVL には、コード分析と静的ドライバー検証ツールのログ ファイルからの結果の要約が含まれています。 ログ ファイルには、ソース コードの情報は含まれていません。

最善の結果を得るには、静的ドライバー検証ツールを実行する前に、コード分析ツールを実行します。

**静的ドライバー検証ツールのログ ファイルを作成するには**

1.  Microsoft Visual Studio Ultimate 2012 でドライバー プロジェクト ファイルを選び、右クリックしてプロジェクトのプロパティを開きます。 **[構成]** として **[Windows 8 Release]\(Windows 8 リリース\)** を選び、 **[プラットフォーム]** として **[x64]** を選びます。
2.  既にコード分析ツールを実行してある場合は、「[静的ドライバー検証ツールの実行](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running_static_driver_verifier)」での手順に従ってください。 SDV の使い方について詳しくは、「ドライバーの不具合を見つけるための静的ドライバー検証ツールの使用」をご覧ください。
3.  SDV によってドライバーの欠陥が見つかった場合、ルール違反の原因になったコード パスのトレースを表示するには、結果ウィンドウで欠陥をクリックします。 ドライバーで見つかったすべての欠陥を修正し、もう一度 SDV を実行します。

静的ドライバー検証ツールでは、プロジェクトの SDV サブディレクトリ (たとえば \\myDriverProject\\SDV) の SDV.DVL.xml ファイルに結果が書き込まれます。

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>解説


静的ドライバー検証ツールとドライバーの検証ツール ログに関する最新情報については、WDK リリース ノートをご覧ください。 リリース ノートは、[Windows Driver Kit (WDK) のダウンロード ページ](https://go.microsoft.com/fwlink/p/?linkid=254897)で入手できます。

**重要**   DVL ファイルでタイムアウト、領域不足などの失敗した結果があっても、認定用に申請できます。 これにより、HCK の静的ツール テストに不合格になることはありません。 HCK 2.0 では、Static Tools (静的ツール) テストに必要なのは、コード分析と SDV が実行されたことを示す DVL ファイルだけです。必ずしもすべてのルールに合格する必要はありません。

 

静的ドライバー検証ツールは、Visual Studio のコマンド プロンプト ウィンドウから実行することもできます。 以下のいずれかのバッチ ファイルを実行して、環境を設定します。

```cpp
"C:\Program Files\Microsoft Visual Studio 11.0\VC\vcvarsall.bat" x64
```

\- または -

```cpp
"C:\Program Files (x86)\Microsoft Visual Studio 11.0\VC\vcvarsall.bat" x64
```

静的ドライバー検証ツールを実行します。

```cpp
msbuild.exe <vcxprojectfile> /p:Configuration="Win8 Release" /p:Platform=x64 /target:sdv /p:inputs="/clean"
msbuild.exe <vcxprojectfile> /p:Configuration="Win8 Release" /p:Platform=x64 /target:sdv /p:inputs="/check:default.sdv"
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


* [ドライバー検証ツール ログの作成](creating-a-driver-verification-log.md)
* [静的ドライバー検証ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)
* [ドライバーの不具合を見つけるための静的ドライバー検証ツールの使用](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)
* [ハードウェア認定プログラム](https://go.microsoft.com/fwlink/p/?linkid=227016)
 

 






