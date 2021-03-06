---
title: 忠実度の高い印刷出力
description: 忠実度の高い印刷出力
ms.assetid: 37ff186e-d078-40f4-b7dc-9bf75e0b2847
keywords:
- 色の忠実性 WDK XPSDrv
- WDK XPSDrv の忠実性を印刷します。
- 信頼性の高い印刷出力 WDK XPSDrv
- XPSDrv プリンター ドライバー WDK、信頼性の高い印刷出力
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d304940921850603c4ed84ef85b5f78ce0e535a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360526"
---
# <a name="high-fidelity-print-output"></a>忠実度の高い印刷出力


XPS ベースのプリンターには、全体的な改善された印刷と色の忠実性を提供できます。 XPS 印刷パスを縮小または可能であれば、常に、イメージのデータ変換と色空間の変換を排除エンドユーザーは、Windows Presentation Foundation (WPF) または XPS ベースのプリンターまたはドライバーに直接出力上に構築されたアプリケーションから印刷するときにそのため、印刷出力には、その元の忠実性を保持できます。

XPS 印刷では、XPS でこれらの属性のネイティブ サポート スプール ファイル形式がグラデーションと透明度などのグラフィックス属性のより忠実なレンダリングを提供します。 XPS ドキュメント形式での XAML は WPF XAML との互換性です。 ユーザーは、WPF アプリケーションから印刷するとき、Windows オペレーティング システムをアニメーションに変換し、ビデオ、および 3 次元 (3 D) 要素のイメージを削除します。 その他のすべてのグラフィック データは、デバイスの使用量に最適な互換性のあるグラフィックス プリミティブで表現されます。 デバイスまたはドライバーは、WPF の出力の印刷バージョンを直接処理します。

XPS ベースのデバイスとドライバーを Microsoft Win32 ベースのアプリケーションからの出力の自動変換、中に印刷の忠実性は GDI + での透過性のシミュレーションに使用される特定の GDI ラスター オペレーション (Rop) を最適化することによって拡張し、グラデーションします。 アプリケーションでは、Rop を使用する代わりにビットマップを生成する場合は、この最適化を実行できません。

XPS の GDI に変換パスは GDI + を使用して、すべてのアプリケーションで似たような実装よりも優れていますが、XPS ベースのプリンターに印刷する WPF アプリケーションから印刷の忠実性も向上します。 XPS-GDI への変換パスでは、GDI ラスター オペレーションと PostScript ビットマスクを使用せずに可能な限り、WPF のグラフィックス代数的透明度 (色とイメージと不透明度、キャンバス上の不透明度マスクでは、アルファ チャネル) の削除を試みます。

 

 




