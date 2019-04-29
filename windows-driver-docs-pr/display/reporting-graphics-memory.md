---
title: グラフィックス メモリのレポート
description: グラフィックス メモリのレポート
ms.assetid: a8a3dc08-1863-47ac-b41e-58ef38739c42
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fdd097bd4d790fca517556d041a6bab2ac39d376
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383271"
---
# <a name="reporting-graphics-memory"></a>グラフィックス メモリのレポート


ビデオ メモリ マネージャーは、ディスプレイのミニポート ドライバーを提供するメモリ情報の詳細をクライアントに報告します。

Windows Vista より前のオペレーティング システム、コントロール パネルの 1 つの数値としてグラフィックス メモリに関するレポート**表示**アプリケーション。 ディスプレイ ドライバーは、この数は、オペレーティング システムを提供します。オペレーティング システムは、を介してユーザーに、数を報告するし、**表示**アプリケーション。

ビデオ メモリ マネージャー、 [Windows Display Driver Model (WDDM)](windows-vista-display-driver-model-design-guide.md)各グラフィックス メモリの共同作成者の正確なアカウントをレポートします。 次のクライアントは、このレポートを使用します。

-   Windows システム評価ツール (WinSAT) では、使用可能なグラフィックス メモリをチェックし、オフにするか、使用可能なメモリの量に基づいて、Aero グラスを Premium エクスペリエンスを有効にするアクションを実行します。

-   デスクトップ ウィンドウ マネージャー (DWM) (Dwm.exe) は、コンピューターで使用可能なグラフィックス メモリの正確な状態によって異なります。 [Windows 表示 Driver Model (WDDM)](windows-vista-display-driver-model-design-guide.md)ドライバーを表示します。

-   Microsoft DirectX ゲームやその他のグラフィックス アプリケーションはグラフィックス メモリの状態を記述する正確な値を取得できる必要があります。 不正確なグラフィックスのメモリ番号では、ユーザーのゲーム エクスペリエンスが大幅に変わります。

次のセクションは、ビデオ メモリ マネージャーがグラフィックス メモリの数値を計算する方法について説明し、メモリの数値を報告する方法の例を指定します。

[グラフィックス メモリを計算します。](calculating-graphics-memory.md)

[例のグラフィックス メモリ レポート](examples-of-graphics-memory-reporting.md)

[グラフィックス メモリの数値を取得します。](retrieving-graphics-memory-numbers.md)

 

 





