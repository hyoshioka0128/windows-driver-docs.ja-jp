---
title: 一般的な説明の言語
description: 一般的な説明の言語
ms.assetid: 818037fd-90bb-46dd-a2e3-239d57ed5fcf
keywords:
- プリンター構成 WDK、GDL ファイル
- テキスト ファイル WDK GDL ファイルします。
- 一般的な説明の言語 WDK
- GDL WDK
- GDL WDK, 概要
- 一般的なプリンター説明 WDK Unidrv
- GPD WDK
- プリンター ドライバー WDK、ジェネリックの説明の言語
- プリンター ドライバー WDK、データを XML に変換します。
- WDK GDL の XML データを変換します。
- XML の WDK GDL にデータを変換します。
- GDL WDK、パーサー
- GDL WDK、スナップショット
- WDK GDL のスナップショット
- GDL WDK、ディレクティブ
- WDK GDL ディレクティブ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c94725649daf146315fbd95109b4e0b4ee4866c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528130"
---
# <a name="generic-description-language"></a>一般的な説明の言語


ジェネリックの説明の言語 (GDL) は、階層的に構造化データを表現する構文を定義します。 GDL は、製造元とコンシューマーを協調的なデータを表現する方法を標準化するために使用できるスキーマを定義することもできます。 このスキーマは、構造とデータの形式を検証し、別の形式 (XML) などに、データの変換を使用できます。

Microsoft が提供、 [GDL パーサー](gdl-parser.md)と関連付けられた*パーサー フィルター*、データ ソースからデータにアクセスして、プロセスがファイルし、階層データに変換する、 [GDL 構文](gdl-syntax.md)を定義します。 GDL には、複雑なデータ セット、オブジェクト指向の構造と、このデータとベンダーによって簡単に拡張するためのメカニズムの処理を定義するスキーマがサポートしています。

GDL がジェネリックのプリンターの説明のスーパー セットとして設計されています ([GPD](introduction-to-gpd-files.md)) 言語で、Unidrv ミニドライバーのプリンターの機能について説明するために使用します。

GDL では、次の主な機能があります。

-   GDL は GPD レガシ形式との下位互換性です。

-   GDL は任意に拡張できます。 すべてのユーザーのカスタム属性と構成要素を追加できます。

-   GDL では、テンプレートを使用して、データの構造を提供します。

-   GDL では、プリプロセッサ ディレクティブと柔軟なリンクを提供するには、構成のパラメーターに基づく条件を使用します。

-   GDL では、データの入力を解析し、クライアントに XML ストリームを返します。

ときに内のデータを[GDL ソース ファイル](gdl-source-files.md)によって解析されます、 [GDL パーサー](gdl-parser.md)パーサーは階層データ構造を保持します。 クライアントから間接的に解析されたデータ構造にアクセスする[スナップショット](gdl-snapshots.md)します。 *スナップショット*は特定の状態でデータを表したものです。 この状態がで指定された、[構成](gdl-configurations.md)します。 GDL パーサーの現在の実装では、スナップショットは、XML として表現し、スナップショット内のデータは、XML ツールを使用してアクセスできます。

GDL パーサーがキーワードを認識するだけでなく、データ エントリ (と呼ばれる[ディレクティブ](gdl-directives.md))。 ディレクティブは、カテゴリをなどがあります[プリプロセッサ](gdl-source-file-preprocessor-directives.md)、[マクロ](gdl-directives-for-macros.md)、[名前空間](gdl-directives-for-namespaces.md)、[テンプレート](gdl-directives-for-templates.md)、および[構成](gdl-directives-for-configurations.md)します。

次のセクションは、GDL の詳細についてを説明します。

[GDL アーキテクチャ](gdl-architecture.md)

[GDL プログラミング ガイド](gdl-programming-guide.md)

[GDL 参照](gdl-reference.md)

[GDL 例](gdl-examples.md)

 

 




