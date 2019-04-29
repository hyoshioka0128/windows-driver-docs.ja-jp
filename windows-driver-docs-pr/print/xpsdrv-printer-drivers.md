---
title: XPSDrv プリンター ドライバー
description: XPSDrv プリンター ドライバー
ms.assetid: 9e61cb21-4e02-48dc-b291-576d37bb640d
keywords:
- XPSDrv プリンター ドライバー WDK、XPS について
- プリンター ドライバー WDK、XPSDrv
- XML の用紙の仕様の WDK の印刷
- XPS ドキュメントの WDK XPSDrv
- XPS スプール ファイル WDK XPSDrv
- WDK のスプール ファイルを印刷します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c821b81b00cb315987fa849590330d432578fdb5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390226"
---
# <a name="xpsdrv-printer-drivers"></a>XPSDrv プリンター ドライバー


XPSDrv プリンター ドライバーでは、XML Paper Specification (XPS) ドキュメントの使用をサポートするバージョン 3 プリンター ドライバー アーキテクチャの Microsoft の GDI ベースを拡張します。 XPSDrv プリンター ドライバーにより、XPS ドキュメント形式はスプール ファイル形式としてもドキュメント ファイル形式としても使われます。

### <a name="overview-of-xps"></a>XPS の概要

XML Paper Specification (XPS) ドキュメントと Windows Vista の印刷機能強化についての基盤となっています。 この仕様では、構造化、XML ベースのドキュメント形式を使用して固定形式のドキュメントの外観について説明します。

XPS ドキュメント形式は、ドキュメントのレイアウトと表示または印刷ドキュメントの表示規則と共に、各ページの視覚的な外観を定義する XML マークアップで構成されます。

### <a name="introduction-to-xps-for-printing"></a>XPS 印刷の概要

XPS ドキュメント形式は、ドキュメント形式、スプール ファイル形式、およびプリンターのページ記述言語 (PDL) として機能します。 ドキュメントのサイクル全体で一貫して XPS を使用する場合は、印刷の予測可能性と信頼性を大幅に向上できます。 スプール ファイル形式と PDL はドキュメントの形式が同じ忠実性とパフォーマンスが向上します。 「わかる is what you get」(WYSIWYG) エクスペリエンスを提供できるように印刷処理全体で XPS ドキュメント形式を使用すると、ドキュメント形式変換を実行するアプリケーションと、プリンターの間の必要があります。

XPS のスプール ファイルは、XPS ドキュメント形式を使用します。 XPS のスプール ファイルはオープンで拡張性とプラットフォーム サービスを使用して表示できます、ドキュメント ワークフローに再導入することができます。

XPS ドキュメントの記述に XPS スプール ファイル内のマークアップは、Extensible Application Markup Language (XAML) マークアップでは、Windows Presentation Foundation (WPF) と互換性が。 そのため、XPS のスプール ファイルに記載されているドキュメントを表示できますネイティブ WPF のデータや正確さを失うことがなく変換は必要ありませんので。 XPS のスプール ファイル内の XAML タグは、WPF の既存のレンダリング クラスの XAML 表現です。 XPS ドキュメント形式は、「印刷」の形式と同じアプリケーションのコンテンツとユーザーの目的を効果的に保持されます。

このセクションの内容:

[XPS 印刷機能](xps-printing-features.md)

[Windows 印刷パスの概要](windows-print-path-overview.md)

[以前のバージョンの Windows での XPS のサポート](xps-support-in-earlier-versions-of-windows.md)

プリンター ドライバー開発者向けの XPS 印刷については詳細は、「 [XPSDrv プリンター ドライバー](xpsdrv-printer-driver.md)します。
