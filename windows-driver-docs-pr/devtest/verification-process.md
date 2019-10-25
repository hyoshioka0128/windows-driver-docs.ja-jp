---
title: 検証プロセス
description: 検証プロセス
ms.assetid: 3803771b-94ef-4e02-9d08-8703283b3f99
keywords:
- 静的ドライバー検証ツール WDK、検証プロセス
- StaticDV WDK、検証プロセス
- SDV WDK、検証プロセス
- 検証プロセス WDK 静的ドライバー検証ツール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d15ee235b36f289beba583f682de367f4d6c9fa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839987"
---
# <a name="verification-process"></a>検証プロセス


SDV*は、ドライバー*の実際の動作が適切な動作を定義する規則に準拠しているかどうかを確認するテストを行います。

ドライバーを確認するコマンドを送信すると、SDV は3段階のプロセスを実行します。このプロセスでは、必要なファイルを特定し、ファイルを準備して、ドライバーを検証します。

このトピックでは、検証プロセスの各手順の動作について説明します。

### <a name="span-idbuildspanspan-idbuildspanbuild"></a><span id="build"></span><span id="BUILD"></span>建設

**ビルド**手順では、Sdv は MSBuild を使用してドライバーをコンパイルし、リンクし、ビルドします。

### <a name="span-idscanspanspan-idscanspanscan"></a><span id="scan"></span><span id="SCAN"></span>取り込む

**スキャン**ステップ中に、sdv は、関数ロールの種類の宣言についてドライバーのコードをスキャンし、ドライバーのエントリポイントの一覧をアセンブルし、ドライバーの*ソース*ファイルを格納するディレクトリに[sdv マップ .h](sdv-map-h.md)ファイルを作成します (**ドライバーのソースディレクトリ**)。

### <a name="span-idcheckspanspan-idcheckspancheck"></a><span id="check"></span><span id="CHECK"></span>オフ

この**チェック**手順では、sdv は検証用に選択したルールを使用してドライバーを準備し、検証します。 選択できる規則の詳細については、「[静的ドライバーの検証規則](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

SDV は、選択した規則にオペレーティングシステムモデルの追加コンポーネントが必要かどうかを判断することから始まります。 その場合、SDV は追加のオペレーティングシステムモデルファイルをドライバーのソースディレクトリにコピーします。

次に、ドライバーファイル、ライブラリファイル、規則コード (*RuleName*) ファイル、およびオペレーティングシステムモデルファイルが、検証のために1つの実行可能ファイルにリンクされます。

次に、SDV 検証エンジンは、選択したすべてのルールが検証されるまで、一度に1つのルールを検証します。

この手順では、SDV は、 *DriverPath*\\SDV\\check ディレクトリで検証された各ルールのサブディレクトリを作成します。

### <a name="span-idcommentspanspan-idcommentspancomment"></a><span id="comment"></span><span id="COMMENT"></span>関する

SDV は検証プロセスのステップを実行しますが、コマンドラインにステータスメッセージを書き込み、各ステップで発生したエラーを報告するエラーメッセージを書き込みます。 ステータスメッセージの詳細については、「[コマンドライン出力](command-line-output.md)」を参照してください。 エラーメッセージの詳細については、「 [Static Driver Verifier Error messages](static-driver-verifier-error-messages.md)」を参照してください。 SDV に関する問題のトラブルシューティングに役立つ診断を有効にする方法については、「[静的ドライバーの検証ツール診断](static-driver-verifier-diagnostics.md)」を参照してください。

 

 





