---
title: Static Driver Verifier の入力ファイル
description: Static Driver Verifier の入力ファイル
ms.assetid: 0c31a752-6946-4704-aff6-c9cd1bf9f522
keywords:
- Static Driver Verifier WDK、入力ファイル
- StaticDV WDK では、入力ファイル
- SDV の WDK、入力ファイル
- 入力ファイル WDK Static Driver Verifier
- WDK Static Driver Verifier のファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d79e38c64ac7365e4cc9e562ba07d93d00dd0e8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538406"
---
# <a name="static-driver-verifier-input-files"></a>Static Driver Verifier の入力ファイル


SDV[検証エンジン](verification-engine.md)検証への入力として、次のファイルを受け取ります。 ドライバーのソース ファイルとオペレーティング システムのモデル ファイルのみの検証にすべての必要です。

-   ドライバーのプロジェクト ファイルとソース コード。 プロジェクト ファイルが配置されているディレクトリに SDV を実行します。

-   [オペレーティング システムのモデル ファイル](operating-system-model.md)します。 SDV は、選択し、検証用に選択したルールに基づいて、オペレーティング システムのモデル ファイルをアセンブルします。

-   [ライブラリ ファイルの処理](library-processing-in-static-driver-verifier.md)します。 ライブラリ ファイルが、ドライバーは、システム以外のライブラリに依存する場合にのみ必要です。 情報と手順については、Static Driver Verifier でライブラリの処理を参照してください。

-   [規則の一覧ファイル](static-driver-verifier-rule-list-file.md)します。 参照してください[Static Driver Verifier のコマンド (MSBuild)](-static-driver-verifier-commands--msbuild-.md)します。

-   [Static Driver Verifier のオプション ファイル](static-driver-verifier-options-file.md)します。 SDV は、SDV の検証にすべてに適用される設定を含むグローバル オプション ファイルを作成します。 ドライバーのオプションのローカル ファイルを作成するには、グローバル オプション ファイルをコピーします。 ドライバーのオプションのローカル ファイルを作成するグローバル オプション ファイルのコピーを編集できます。

SDV の検証の結果を評価するときに、精度と検証で使用されていたすべての入力ファイルの完全性を確認する入力ファイルを確認することが重要です。

このセクションには、次のファイルの詳細な説明が含まれています。

[Static Driver Verifier ルール リスト ファイル](static-driver-verifier-rule-list-file.md)

[Static Driver Verifier のオプション ファイル](static-driver-verifier-options-file.md)

 

 





