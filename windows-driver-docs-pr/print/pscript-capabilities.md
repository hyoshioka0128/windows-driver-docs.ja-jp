---
title: Pscript 機能
description: Pscript 機能
ms.assetid: 1530cb64-a1b1-4ff5-a6bf-b3634e83a225
keywords:
- PostScript プリンター ドライバー WDK、印刷機能
- Pscript WDK、印刷機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7729dfa4f62b93aaed391ed613864e31c06009d5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571295"
---
# <a name="pscript-capabilities"></a>Pscript 機能





PostScript プリンター ドライバー (Pscript) は、次の機能を提供します。

-   特定のプリンターを使用して、すべての PostScript プリンターのサポート*PPD*-ベース[Pscript ミニドライバー](pscript-minidrivers.md)各プリンターの特性を記述します。

-   A [Pscript ユーザー インターフェイス](pscript-user-interface.md)を基に、TreeView コントロールとプロパティ シート、一貫性のあるすべてのプリンターが各プリンターの固有のオプションの変更可能になります。

-   1 つ[Pscript レンダラー](pscript-renderer.md)の GDI グラフィックス エンジンと共に変換 Microsoft Win32 GDI 呼び出しアプリケーションから印刷スプーラに送信できるプリンター コマンドにします。

-   ドキュメント構造の規則、Adobe Systems, Inc. によって公開された PostScript 言語のリファレンス マニュアルで説明されているのバージョン 3.1 のサポート

-   PostScript レベル 1、レベル 2、またはレベル 3 の機能を提供するプリンターをサポートします。

-   フォントのサポートの次の種類:
    -   増分ダウンロード OpenType フォントの PostScript 型 1 または 2 の種類 として。
    -   増分ダウンロード TrueType フォントのフォントの PostScript Type 1、種類 3、型 32、Type 42 の場合、または Type 42 の CID ベースとして。
    -   増分のホストに常駐ラスター フォントとしてダウンロード PostScript タイプ 3 または型 32 のフォント。
    -   完全なホストに常駐 PostScript Type 1 フォントのダウンロードしています。
    -   PostScript Type 1、2、および CID フォントをプリンターに常駐します。
    -   ごとのプリンターの文字セット内に存在するグリフのグリフのフォントの置き換え
-   ホスト システム上またはプリンターのハードウェアで実行するには、ICM 2.0、および許可イメージ カラーの管理をサポートします。

 

 




