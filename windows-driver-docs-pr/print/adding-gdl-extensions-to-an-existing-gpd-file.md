---
title: 既存の GPD ファイルに GDL 拡張機能を追加する
description: 既存の GPD ファイルに GDL 拡張機能を追加する
ms.assetid: 5ba2a447-e133-47bb-aa1e-93abe75c6eef
keywords:
- ボックスの自動構成サポート WDK プリンター、GDL 拡張機能
- GDL ファイル WDK プリンター
- WDK GDL ファイルの拡張機能
- GPD は、WDK GDL 拡張機能をファイルします。
- GPD ファイル WDK GDL 拡張機能を追加します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0203fdc2e83181272e8ebf43e658df2a224a43c2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341332"
---
# <a name="adding-gdl-extensions-to-an-existing-gpd-file"></a>既存の GPD ファイルに GDL 拡張機能を追加する


既存のインボックス GPD ファイルを自動構成サポートを追加する場合は、次の操作をする必要があります。

1.  GDL ファイルを作成します。 GDL ファイルである必要があります、  **\*BidiQuery**と **\*BidiResponse**に対応する要素、 **\*機能**/**\*オプション**PPD ファイルで指定された構成要素。 双方向の情報を必要とする機能にのみこれらの要素を追加する必要がありますに注意してください。

2.  ドライバーに依存するファイル リストの一部として GDL ファイルが含まれます。

このセクションの内容:

[GPD スキーマの新しいキーワード](new-keyword-for-gpd-schema.md)

[Windows Vista で GPD のフローを自動構成](autoconfiguration-flow-for-gpd-in-windows-vista.md)

[GDL ファイル GPD の構成要素を追加します。](adding-constructs-to-your-gdl-file-for-gpd.md)

 

 




