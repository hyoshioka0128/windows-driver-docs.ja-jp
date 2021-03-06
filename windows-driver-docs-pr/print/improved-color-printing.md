---
title: 強化されたカラー印刷
description: 強化されたカラー印刷
ms.assetid: b0487ee0-9b4a-4083-9416-ad22b97ed94b
keywords:
- XPSDrv プリンター ドライバー WDK、カラー印刷
- 印刷の WDK XPSDrv を色します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b16cfe7f7e3ca4a0c8902720526800619d8336ea
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392825"
---
# <a name="improved-color-printing"></a>強化されたカラー印刷


新しい色の管理機能と、XPS、豊富なより予測可能なカラー印刷を提供する作業を Windows Vista でのパスを印刷します。 拡張されたカラー サポートでは、4 つを超える材で印刷をサポートすることでハイエンドの印刷ができます。 (4 つを超える材は、出力アプリケーションと顧客に必要)。新しい XPS 印刷アーキテクチャでは、全体の色域プリンターに拡張カラーのアプリケーションによって生成される情報と通信できます。 デバイス ドライバーにアクセスできると印刷のパイプラインから色の情報を制御します。

Windows Vista は信頼性が高く、別のソフトウェア アプリケーション、イメージング デバイス、イメージング メディア、および、予測可能な表示条件の間で色を一致するように色の管理に重要な技術革新を導入するには、Windows の色のシステムの完全な使用により、一貫した方法。 XPS ドキュメントでは、XPS ドキュメント ベースのデバイスにアプリケーションの色の情報を送信するためのパイプです。 XPS ドキュメント形式では、次のネイティブ サポートにより、このテクノロジが適用されます。

-   高い有効桁数、以上のダイナミック レンジおよび域色空間を拡大します。

-   CMYK (で 4 つ材より大きい)、n インク システムのサポートの使用。

-   名前付きの色をサポートします。

XPS のスプール ファイルを通じて XPS 印刷パスは、デバイス ドライバーに直接この高度なカラー情報を提供します。 必要に応じて、デバイス ドライバーは、次の強化された色の処理を提供できます。

-   XPS を使用したデバイスの色の自動構成は印刷ドライバーのパスです。

-   別の印刷デバイス用のパイプライン内のコンテンツを再利用する機能。

-   カラー プロファイルと処理命令は、スプール ファイルに直接埋め込むことがあるため、アプリケーションからドライバーに色のデータを確実に永続化する機能。

-   色の機能と設定の通信を強化します。 アプリケーションでは、色にすることで、新しい印刷パスのシステム色の管理を無効にする処理を制御できます。 ドライバーは、自分のデバイスの色の機能をより完全に表現できます。

 

 




