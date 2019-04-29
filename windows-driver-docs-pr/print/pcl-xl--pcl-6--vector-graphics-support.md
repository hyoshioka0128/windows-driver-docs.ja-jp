---
title: PCL XL (PCL-6) ベクトル グラフィックス サポート
description: PCL XL (PCL-6) ベクトル グラフィックス サポート
ms.assetid: c8a96506-ed95-44f2-863e-24cbfc919d65
keywords:
- ベクター グラフィックス WDK Unidrv、PCL XL
- PCL XL ベクター グラフィックス WDK Unidrv
- PCL XL ベクター グラフィックスに関する PCL XL の WDK Unidrv ベクター グラフィックス
- PCL-6 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a78a59cc42ce54e3d8bff47c04dfca0cc0a71ef
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390920"
---
# <a name="pcl-xl-pcl-6-vector-graphics-support"></a>PCL XL (PCL-6) ベクトル グラフィックス サポート





Unidrv Windows XP 以降では、PCL XL 白黒のグラフィックスがサポートされています。 Unidrv Windows Server 2003 以降では、PCL XL 色グラフィックスがサポートされています。

PCL XL (PCL 6) のベクター グラフィックスの Unidrv のサポートにより純粋ラスター形式の代替として PCL XL 形式でジョブのデータを作成できます。 PCL XL 形式であり、デバイスの場合、通常、最適なシステム オーバーヘッドが少ない、出力データ、および高速な印刷スループット以下では通常になります。

PCL XL では、ジョブの設定、ページ設定、メディアの選択、および用紙サイズを GPD 現在定義されている機能のほとんどを使用します。 ただし、実際の描画コマンドでは Unidrv 内にハードコーディングします。 その結果、GPD ファイル内のほとんどの描画コマンドは無視されます。 GPD ファイルからこれらのコマンドを削除する必要はありません。

このセクションでは、次のトピックについて説明します。

[PCL XL GPD ファイルへの書き込み](writing-a-pcl-xl-gpd-file.md)

[PCL XL ミニドライバーの色のサポートを有効にします。](enabling-support-for-color-in-pcl-xl-minidrivers.md)

[PCL XL ミニドライバーで新しいデバイス フォントを指定します。](specifying-new-device-fonts-in-pcl-xl-minidrivers.md)

[既定の PCL XL のフォントを使用します。](using-default-pcl-xl-fonts.md)

[PCL の XL ミニドライバーをインストールします。](installing-a-pcl-xl-minidriver.md)

[PCL XL の問題](pcl-xl-issues.md)

 

 




