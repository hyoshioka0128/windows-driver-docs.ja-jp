---
title: 静的ドライバー検証ツールの診断
description: 静的ドライバー検証ツールの診断
ms.assetid: dff22144-43a0-427f-8075-9c9152670933
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f5ddebd0f0141e18d32c574cae767b2fa3e890d
ms.sourcegitcommit: 87975bf11f43410ae113b57a34131778fb9677a0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2019
ms.locfileid: "72549716"
---
# <a name="static-driver-verifier-diagnostics"></a>静的ドライバー検証ツールの診断


SDV には、SDV によって発生する可能性のある問題のトラブルシューティングに役立つ診断モードがあります。 診断モードが有効になっている場合、SDV は、検証とルールごとに1つずつ、ドライバープロジェクトの一連のファイルにメッセージを記録します。

### <a name="span-idenabling_diagnosticsspanspan-idenabling_diagnosticsspanenabling-diagnostics"></a><span id="enabling_diagnostics"></span><span id="ENABLING_DIAGNOSTICS"></span>診断の有効化

現在、SDV (デバッグモードとも呼ばれます) の診断モードは、コマンドラインから実行している場合にのみ有効にすることができます。  コマンドラインからの実行の詳細については、「 [Static Driver Verifier commands (MSBuild)](-static-driver-verifier-commands--msbuild-.md)」を参照してください。

診断をアクティブ化するには、 **/チェック**コマンドの後に **/debug**フラグを追加します。  次に、例を示します。

```
msbuild /t:sdv /p:Inputs="/check:* /debug" mydriver.VcxProj /p:Configuration="Release" /p:Platform=x64
```

診断を有効にすると、特定のログファイルの作成だけでなく、コマンドウィンドウへの出力も大幅になります。

### <a name="span-idenabling_diagnosticsspanspan-idenabling_diagnosticsspanunderstanding-diagonistics"></a><span id="enabling_diagnostics"></span><span id="ENABLING_DIAGNOSTICS"></span>Diagonistics について

SDV は、実行の各ステージに複数のファイルを作成し、その手順について詳しく説明します。  SDV が実行の途中で失敗した場合、後でステージするために diagonistic ファイルは作成されません。

作成されるファイルの順序は次のとおりです。
* **smvexecute-NormalBuild**: ドライバーのソースディレクトリにあり、追加のインストルメンテーションと分析を行わずに、ドライバーをビルドするための sdv の初期試行の出力が表示されます。
* **smvexecute-InterceptedBuild**: これは、ドライバーのソースディレクトリにあり、分析フックが追加された sdv の出力を示しています。  
* **smvcl .log**: これは、ドライバープロジェクトで sdv によって作成された "sdv" ディレクトリにあります。  InterceptedBuild ステップのコンパイラ出力が表示されます。  **Smvexecute-InterceptedBuild**でエラーが発生した場合は、 **smvcl .log**で詳細を確認できる場合があります。

* **smvexecute-Scan**: これは、ドライバープロジェクトで sdv によって作成された "sdv" ディレクトリにあります。  エントリポイントを見つけるために、ドライバーをスキャンする SDV の出力を示します。  ここでのエラーは、エントリポイントが見つからなかったことを示している可能性があります。関数 roletypes または sdv-map. h を更新する必要があります。  詳細については、「[関数ロール型宣言の使用](using-function-role-type-declarations.md)」および「 [Sdv .H ファイルの承認](approving-the-sdv-map-h-file.md)」を参照してください。
* **smvexecute-FinalCompile**: sdv によって検証されたルールごとに、これらのファイルの1つが作成されます。これは、ドライバープロジェクトで "sdv\ check \[rule name]" サブフォルダー sdv によって作成されます。  このファイルには、OS モデルと特定のルールを使用してドライバーをビルドする SDV の出力が表示されます。  
* **smvexecute-CheckRule**: sdv によって検証されたルールごとに、これらのファイルの1つが作成されます。これは、ドライバープロジェクトで "sdv\ check \[rule name]" サブフォルダー sdv によって作成されます。  このファイルは、ドライバーに対して指定された規則を確認する SDV の試行の出力を示します。

コマンドの出力で、ステージングリストに対応するファイルを [失敗] として検索する必要があります。  **Finalcompile**または**checkrule**の手順でエラーが発生した場合は、[失敗] と表示されている特定のルールのフォルダーを確認してください。
