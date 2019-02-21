---
title: PDB シンボル ファイル
description: PDB シンボル ファイル
ms.assetid: 077784d9-06be-450c-bdd5-02321305df1b
keywords:
- プログラム データベース シンボル ファイル WDK
- PDB シンボル ファイルの WDK
- シンボル ファイルの WDK ソフトウェア トレース
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 482df3ee811b54185e4e48f9b9df6fc064ad0880
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559629"
---
# <a name="pdb-symbol-files"></a>PDB シンボル ファイル


## <span id="ddk_pdb_symbol_files_tools"></span><span id="DDK_PDB_SYMBOL_FILES_TOOLS"></span>


プログラム データベース (PDB) シンボル ファイルを[トレース プロバイダー](trace-provider.md)など、アプリケーションまたはドライバーの人間が判読できる表示を表示するように、トレース メッセージを書式設定するための手順が含まれています。

トレース メッセージの書式設定手順については、トレース プロバイダーのソース コードの一部です。 [WPP プリプロセッサ](wpp-preprocessor.md)コードからそれらを抽出し、トレース プロバイダーの PDB シンボル ファイルに追加します。

コンパイラは、トレース プロバイダーのデバッグ (オン) バージョンをコンパイルするときに、PDB ファイルを生成します。 使用する場合、ビルド処理が既定では PDB ファイルを作成[BinPlace](binplace.md)トレース プロバイダーを作成します。

[トレース コンシューマー](trace-consumer.md) 、WDK で[traceview で](traceview.md)と[Tracefmt](tracefmt.md)、書式設定情報を PDB ファイルから直接または TMF ファイルからのトレース メッセージを抽出することができます。 他のユーザーには、TMF ファイルが必要です。 [Tracepdb](tracepdb.md) PDB ファイルを入力として受け取り、書式設定の情報を抽出し、出力として TMF ファイルを作成します。

Tracerpt、Windows に含まれるツールなど、他のトレース コンシューマーでは、PDB ファイルまたは TMF ファイルは使用しないでください。 代わりが情報を使用して管理オブジェクト フォーマット (MOF) ファイルでトレース イベントの書式を設定します。 これらのツールは、トレース メッセージを書式設定できません。

 

 





