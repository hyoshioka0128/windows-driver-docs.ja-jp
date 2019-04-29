---
title: プリンター ミニドライバー変更
description: プリンター ミニドライバー変更
ms.assetid: 8f427642-a758-48bf-96e1-95a27adbaf23
keywords:
- ボックスの自動構成サポートの WDK プリンター、ミニドライバーの変更
- GPD ファイル WDK の印刷、インボックスの自動構成サポート
- GDL ファイル WDK プリンター
- PPD ファイル WDK の自動構成
- プラグインを WDK の印刷、インボックスの自動構成サポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29dcdfe0ac9a9b7c8e613af3c4892d78a28e5444
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384603"
---
# <a name="printer-minidriver-changes"></a>プリンター ミニドライバー変更


プリンター ミニドライバーは、プリンターの記述ファイルで構成されています (*GPD*、 *PPD*、または GDL ファイル)、および省略可能なユーザー インターフェイス (UI) プラグイン、レンダリング プラグインと表示フィルター。 ボックスに含めることで、プラグインの 1 つだけの UI が許可されますと 1 つだけ Unidrv または Pscript レンダリング プラグインが許可されています。 IHV のポート モニターは、インボックスでプリンター ミニドライバーとして含まれるは許可されていません。

GPD、PPD、または GDL ファイルには、考慮すべき 2 つのケースがあります。

-   GDL ファイルに追加します。GDL ファイルは、プリンターのデータ ファイルを置き換える GPD PPD ファイルです。

-   プリンター ドライバーは既に Windows に同梱され、GPD ファイルが存在するため、既存の GPD または PPD ファイルまたは PPD ファイルの関連付けを変更します。

次のトピックでは、UI のドライバーとプリンターのデータ ファイル内で行う必要がある変更について説明します。

[UI プラグインの変更](ui-plug-in-changes.md)

[既存の GPD ファイル GDL 拡張機能の追加](adding-gdl-extensions-to-an-existing-gpd-file.md)

[既存の PPD ファイル GDL 拡張機能の追加](adding-gdl-extensions-to-an-existing-ppd-file.md)

[ミニドライバーの INI ファイルの BidiFiles エントリ](bidifiles-entry-in-a-minidriver-s-ini-file.md)

[Pscript と Unidrv ミニドライバーの名前付け規則](naming-conventions-in-pscript-and-unidrv-minidrivers.md)

 

 




