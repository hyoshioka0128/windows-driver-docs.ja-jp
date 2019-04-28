---
title: 検証プロセス
description: 検証プロセス
ms.assetid: 3803771b-94ef-4e02-9d08-8703283b3f99
keywords:
- Static Driver Verifier WDK、検証プロセス
- StaticDV WDK、検証プロセス
- SDV の WDK、検証プロセス
- 検証プロセス WDK Static Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25782357a3f8c7bd9f2b2d0372aa4ce6c6216ecc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379874"
---
# <a name="verification-process"></a>検証プロセス


SDV の実施、*検証*動作が適切な動作を定義するルールに準拠して、ドライバーは実際のかどうかを判断するテストは、します。

ドライバーを確認するためのコマンドを送信するときに SDV を 3 段階のプロセス、ファイル、ファイルを準備、し、ドライバーの検証を決定を実行します。

このトピックでは、各検証プロセスの手順での動作について説明します。

### <a name="span-idbuildspanspan-idbuildspanbuild"></a><span id="build"></span><span id="BUILD"></span>ビルド

中に、**ビルド**手順、SDV のコンパイル、リンク、および MSBuild を使用してドライバーをビルドします。

### <a name="span-idscanspanspan-idscanspanscan"></a><span id="scan"></span><span id="SCAN"></span>スキャン

中に、**スキャン**手順、SDV は、関数の役割の型宣言に対するドライバーのコードをスキャン、ドライバーのエントリ ポイントの一覧をアセンブルし、作成、 [Sdv map.h](sdv-map-h.md) を格納するディレクトリ内のファイル*ソース*ドライバーのファイル (と呼ばれる、**ドライバーのソース ディレクトリ**)。

### <a name="span-idcheckspanspan-idcheckspancheck"></a><span id="check"></span><span id="CHECK"></span>チェック

中に、**確認**ステップ、SDV の準備および検証の選択した規則を使用して、ドライバーを確認します。 選択可能なルールの詳細については、次を参照してください。[静的ドライバー検証規則](https://msdn.microsoft.com/library/windows/hardware/ff551714)します。

SDV は、オペレーティング システムのモデルの追加のコンポーネントを選択した規則が必要かどうかを開始します。 場合は、SDV は、ドライバーのソース ディレクトリに追加のオペレーティング システムのモデル ファイルをコピーします。

次に、ドライバー ファイル、ライブラリのファイルがコードをルール (*RuleName*.slic) ファイル、およびオペレーティング システムのモデル ファイルは、検証のための 1 つの実行可能ファイルにリンクさせます。

SDV 検証エンジンは、選択したすべてのルールを確認するまで、一度に 1 つのルールを確認します。

この手順では、SDV には、各ルールの検証にサブディレクトリが作成されます、 *DriverPath*\\sdv\\ディレクトリを確認します。

### <a name="span-idcommentspanspan-idcommentspancomment"></a><span id="comment"></span><span id="COMMENT"></span>コメント

SDV は、検証プロセスでの手順を実行、中にステータス メッセージに書き込みますエラー メッセージと共にコマンド ラインで発生するエラーを報告する各ステップで。 ステータス メッセージについては、次を参照してください。[コマンド ライン出力](command-line-output.md)します。 エラー メッセージについては、次を参照してください。[静的ドライバー検証ツールのエラー メッセージ](static-driver-verifier-error-messages.md)します。 Microsoft の SDV に関する問題のトラブルシューティングと診断を有効にする方法については、次を参照してください。[静的ドライバー検証ツール診断](static-driver-verifier-diagnostics.md)します。

 

 





