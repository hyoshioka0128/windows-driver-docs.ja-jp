---
title: 既存の PPD ファイルに GDL 拡張機能を追加する
description: 既存の PPD ファイルに GDL 拡張機能を追加する
ms.assetid: 4d425701-85af-43e8-9ff2-ddfcc755f90c
keywords:
- ボックスの自動構成サポート WDK プリンター、GDL 拡張機能
- GDL ファイル WDK プリンター
- WDK GDL ファイルの拡張機能
- PPD ファイル WDK 自動構成、GDL 拡張機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 737178efe7180ccfc87f59c5b1280b97c0e633c7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354108"
---
# <a name="adding-gdl-extensions-to-an-existing-ppd-file"></a>既存の PPD ファイルに GDL 拡張機能を追加する


既存のインボックス PPD ファイルを自動構成サポートを追加する場合は、次の手順に従います。

1.  GDL ファイルを作成します。 GDL ファイルである必要があります、 \* **BidiQuery**と\* **BidiResponse**に対応する要素、 \***機能**/\***オプション**PPD ファイルで指定された構築します。 必要がありますには双方向の情報を必要とする機能に対してのみに注意してください。

2.  ドライバーに依存するファイルの一覧の一部として GDL ファイルが含まれます。

このセクションの内容:

[PPD スキーマの新しいキーワード](new-keyword-for-ppd-schema.md)

[PPD 向け Windows Vista で Autoconfig フロー](autoconfig-flow-in-windows-vista-for-ppd.md)

[GDL ファイル PPD の構成要素を追加します。](adding-constructs-to-your-gdl-file-for-ppd.md)

 

 




