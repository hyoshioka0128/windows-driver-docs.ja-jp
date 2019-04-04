---
title: 静的ドライバー検証ツールの診断
description: 静的ドライバー検証ツールの診断
ms.assetid: dff22144-43a0-427f-8075-9c9152670933
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ffe5655e2916d59eca26b695e569aeeadc22a85f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578186"
---
# <a name="static-driver-verifier-diagnostics"></a>静的ドライバー検証ツールの診断


SDV は、お客様とマイクロソフトの SDV が発生する可能性のある問題のトラブルシューティングに役立つ診断モードです。 診断モードを有効にすると、SDV は、一連のドライバー プロジェクト、およびルールの検証の段階ごとに 1 つのファイルにメッセージを記録します。

### <a name="span-idenablingdiagnosticsspanspan-idenablingdiagnosticsspanenabling-diagnostics"></a><span id="enabling_diagnostics"></span><span id="ENABLING_DIAGNOSTICS"></span>診断を有効にします。

SDV (デバッグ モードとも呼ばれます) は現在の診断モードのみ有効にする、コマンドラインから実行する場合。  コマンドラインからの実行に関する詳細については、[Static Driver Verifier のコマンド (MSBuild)](-static-driver-verifier-commands--msbuild-.md)を参照してください。

診断を有効にするには、追加、 **/debug**フラグを設定した後、 **/check**コマンド。  以下に例を示します。

```
msbuild /t:sdv /p:Inputs="/check:* /debug" mydriver.VcxProj /p:Configuration="Release" /p:Platform=x64
```

診断を有効にすると、詳細出力が大幅にコマンド ウィンドウに特定のログ ファイルの作成とされます。

### <a name="span-idenablingdiagnosticsspanspan-idenablingdiagnosticsspanunderstanding-diagonistics"></a><span id="enabling_diagnostics"></span><span id="ENABLING_DIAGNOSTICS"></span>Understanding Diagonistics

SDV はそのステップの詳細を提供する実行の各段階で複数のファイルを作成します。  SDV は、実行を途中で失敗した場合、後のステージのない diagonistic ファイルが作成されます。

作成されたファイルは、順番は。
* **smvexecute-NormalBuild.log**:これは、ドライバーのソース ディレクトリにあるし、追加のインストルメンテーションや分析を行わず、ドライバーのビルドの SDV の初回試行の出力を示しています。
* **smvexecute-InterceptedBuild.log**:これにより、ドライバーのソース ディレクトリにあるし、SDV analysis フックを追加して、ドライバーをビルドの出力を示しています。  
* **smvcl.log**:これは、SDV で、ドライバーのプロジェクトで作成した"sdv"ディレクトリにあります。  InterceptedBuild ステップのコンパイラの出力が表示されます。  エラーが表示する場合**smvexecute InterceptedBuild.log**で追加の詳細を検索することができます**smvcl.log します。**

* **smvexecute-Scan.log**:これは、SDV で、ドライバーのプロジェクトで作成した"sdv"ディレクトリにあります。  SDV のエントリ ポイントを検索するドライバーをスキャンしようの出力が表示されます。  ここでエラーことを示すエントリ ポイントが見つかりません関数 roletypes または sdv map.h を更新する必要があります。  参照してください[を使用して関数の役割の型の宣言](using-function-role-type-declarations.md)と[Sdv map.h ファイルを承認する](approving-the-sdv-map-h-file.md)詳細についてはします。
* **smvexecute-FinalCompile.log**:これらのファイルの 1 つは、各ルールは、sdv、によって検証しで見つかる用に作成されたが、"sdv\check\[規則名]"サブフォルダー SDV は、ドライバーのプロジェクトで作成します。  このファイルは、SDV の構築しようとする特定のルールと OS のモデルでのドライバーの出力を示します。  
* **smvexecute-CheckRule.log**:これらのファイルの 1 つは、各ルールは、sdv、によって検証しで見つかる用に作成されたが、"sdv\check\[規則名]"サブフォルダー SDV は、ドライバーのプロジェクトで作成します。  このファイルは、ドライバーに対して指定されたルールを検証しようと SDV の出力を示します。

コマンドの出力に失敗のマークを一覧表示する段階に対応するファイルを検索する必要があります。  障害が発生した場合、 **FinalCompile**または**CheckRule**手順、障害が発生したとして、特定のルールのフォルダーをチェックすることを確認して表示をします。
