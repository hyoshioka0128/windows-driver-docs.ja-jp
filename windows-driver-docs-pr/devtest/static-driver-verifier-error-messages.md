---
title: Static Driver Verifier エラー メッセージ
description: Static Driver Verifier エラー メッセージ
ms.assetid: 16fae27c-2495-4b54-9df8-b70ad20d30ab
keywords:
- Static Driver Verifier WDK、エラー
- StaticDV WDK、エラー
- SDV の WDK、エラー
- メッセージ WDK Static Driver Verifier
- エラー WDK Static Driver Verifier
ms.date: 04/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: fdbc8ed12a58a59cbd347c88b1c44b3f4dde888c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532851"
---
# <a name="static-driver-verifier-error-messages"></a>Static Driver Verifier エラー メッセージ


このセクションより頻繁に見られる SDV エラーのいくつかの意味は、メッセージをそれらを解決する方法について説明します。

SDV は Visual Studio からを起動するときに、次のエラーが表示されます。

* **SDV は、非デバッグ構成でのみ動作**:メッセージは、非デバッグ構成に SDV を実行する必要があります。  リリース構成に、プロジェクトが設定されていることを確認または使用できない場合は、1 つを作成、SDV を再度起動してください。
* **使用可能なルールを読み込み中にエラーが発生しました**:SDV は、ドライバーのルールをモデルまたはドライバー モデルを正しく判断できないか見つけることができません (ずっと高い確率で、ドライバーが WDM、KMDF、NDIS、または Storport ドライバーではない場合)。  WDK が正しくインストールされている場合は、SDV を直接コマンドラインから実行して、このエラーを回避することがありますできます (を参照してください[Static Driver Verifier のコマンド (MSBuild)](-static-driver-verifier-commands--msbuild-.md))。
* **SDV は、ドライバーのディレクトリをクリーンアップできませんでした**:場合によっては、アクセス許可のエラーは、[クリーン] ボタンをクリックすると、ドライバー ディレクトリから古い結果を正しくクリーンアップから SDV をできない可能性があります。  このエラーは、以前の実行から sdv ファイルが現在使用されている場合にも発生します。  ドライバー ディレクトリに、SDV ファイルを使用して、何もすることを確認し、"sdv"と"sdv.temp"フォルダーと任意の"staticdv.job"ファイルを削除します。

SDV は、分析を試みているときに失敗した場合、標準出力に失敗したため、ステージが出力されます。  Visual Studio の GUI から SDV を実行するときに、[アラート] タブに切り替えることでこの出力を確認できます。

SDV で失敗する可能性があります段階があります。
* **NormalBuild**:SDV は、標準の MSBuild コマンドを使用してドライバーをビルドできませんでした。  これは、ビルド ロジックの専門的なまたはプロジェクト ファイル内のソリューションの要素の依存コンポーネントが外部のビルドを実行する場合に発生する可能性があります。  プロジェクトは、$ (solutiondir) プロパティに依存する場合は、コマンドラインから SDV を再実行し、追加することで、コマンドラインに追加して直接この変数を指定できます **/p:SolutionDir =\[、ソリューションの dir\]** MSBuild コマンドの末尾にします。  参照してください[Static Driver Verifier のコマンド (MSBuild)](-static-driver-verifier-commands--msbuild-.md)します。
* **InterceptedBuild**:SDV は、分析用のドライバーをビルドできませんでした。  
* **スキャン**:SDV は、ドライバーのエントリ ポイントを検索できませんでした。  ここでエラーことを示すエントリ ポイントが見つかりません関数 roletypes または sdv map.h を更新する必要があります。  参照してください[を使用して関数の役割の型の宣言](using-function-role-type-declarations.md)と[Sdv map.h ファイルを承認する](approving-the-sdv-map-h-file.md)詳細についてはします。
* **FinalCompile**:SDV は、ルールと OS のモデルを使用してドライバーをコンパイルできませんでした。
* **CheckRule**:SDV は、正しく規則を検証できませんでした。

SDV の診断を有効にすると、エラーの詳細を学習することができます。  参照してください[静的ドライバー検証ツール診断](static-driver-verifier-diagnostics.md)詳細についてはします。
