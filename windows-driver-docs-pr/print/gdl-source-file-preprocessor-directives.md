---
title: GDL ソース ファイルのプリプロセッサ ディレクティブ
description: GDL ソース ファイルのプリプロセッサ ディレクティブ
ms.assetid: cc0f807f-5c06-4add-bed1-c15c8251dc98
keywords:
- WDK GDL、ソース ファイルのプリプロセッサ ディレクティブのディレクティブ
- ソース ファイル WDK GDL、プリプロセッサ ディレクティブ
- WDK GDL のプリプロセッサ ディレクティブ
- パーサー WDK GDL、ディレクティブ
- WDK GDL ディレクティブします。
- プリコンパイル済みディレクティブ WDK GDL
- WDK GDL ディレクティブします。
- 未定義の WDK GDL ディレクティブ
- Ifdef ディレクティブ WDK GDL
- Elseifdef ディレクティブ WDK GDL
- Else ディレクティブ WDK GDL
- Endif ディレクティブ WDK GDL
- SetPPPrefix ディレクティブ WDK GDL
- UndefinePrefix ディレクティブ WDK GDL
- EnablePPDirective ディレクティブ WDK GDL
- DisablePPDirective ディレクティブ WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ba7be92d123a993a953bcf7fbb665d9dc5efdc9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536574"
---
# <a name="gdl-source-file-preprocessor-directives"></a>GDL ソース ファイルのプリプロセッサ ディレクティブ


元の GPD パーサーのように、GDL パーサーには、プリプロセッサ ディレクティブがサポートされています。 プリプロセッサ ディレクティブは、その他の解析前に処理されます。 プリプロセス フェーズでは、プリプロセッサ ディレクティブだけが認識され、ディレクティブ以外のすべてのエントリはブラック ボックス データとして扱われます。 前処理のフレーズの中にすべてのプリプロセッサ ディレクティブは、後続の解析フェーズは、プリプロセッサ構文に対処する必要はありませんので、入力ストリームから削除されます。

プリプロセッサ ディレクティブの目的は、GDL または GPD パーサーの複数のバージョンで実行されている単一 GDL ファイルを作成するためです。 使用することができますをいくつかパーサーのバージョンでのみ発生するパーサーの機能がある場合、  **\#Ifdef**ステートメントと同等のエントリにより、機能を置換します。

プリプロセッサ ディレクティブを使用して、特定の[GDL プリプロセッサ構文](gdl-preprocessor-syntax.md)と[GDL プリプロセッサ キーワード](gdl-preprocessor-keywords.md)します。

GDL プリプロセッサ ディレクティブは、GPD プリプロセッサ ディレクティブの拡張機能です。 GDL および GPD のプリプロセッサ ディレクティブの違いの詳細については、次を参照してください。 [GDL 間の相違点と GPD 前処理](differences-between-gdl-and-gpd-preprocessing.md)します。

GDL プリプロセッサ ディレクティブは、1 つだけな GDL ディレクティブです。 GDL ディレクティブの他の種類の詳細については、次を参照してください。 [GDL ディレクティブ](gdl-directives.md)します。

次に、GDL プリプロセッサのキーワードの概要を示します。

-   **\#含める**GDL の現在のファイルに追加するための別の GDL ファイルを参照します。

-   **\#定義**と**\#定義を解除**プリプロセッサ条件付きディレクティブを使用するシンボルの一覧を管理します。

-   **\#プリコンパイル済み**GDL の別のファイルを表す GDL データ構造を動的にリンクされているこのファイルに含まれる GDL ソース ファイルを表すスタンドアロンのデータ構造を作成します。 このディレクティブを使用すると、頻繁に使用されるファイルの冗長コピーを排除します。

-   **\#Ifdef**、  **\#Elseifdef**、  **\#Else**、および **\#Endif**条件付きで、GDL 内のセクションでは無効にします。ソース ファイルです。 これらのディレクティブは、条件付きプリプロセッサ ディレクティブで定義されているシンボルまたは GDL パーサーの各種バージョンで定義されているシンボルを参照できます。

-   **\#SetPPPrefix**、  **\#UndefinePrefix**、  **\#EnablePPDirective**、および **\#DisablePPDirective**ディレクティブの処理を変更します。

このセクションの内容:

[GDL プリプロセッサ構文](gdl-preprocessor-syntax.md)

[GDL プリプロセッサ キーワード](gdl-preprocessor-keywords.md)

[GDL と GPD 前処理の違い](differences-between-gdl-and-gpd-preprocessing.md)

[GDL プリプロセッサ ガイドライン](gdl-preprocessor-guidelines.md)

 

 




