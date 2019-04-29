---
title: ガード バンド クリッピング
description: ガード バンド クリッピング
ms.assetid: bd4ebd97-c948-4219-95a5-f7c6ca45f792
keywords:
- Direct3D WDK Windows 2000 の表示、ガード バンド クリッピング
- WDK の Direct3D をクリッピング guard バンド
- クリッピング WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5099f27c057810350bda7afdc5f341a12fe67f14
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323751"
---
# <a name="guard-band-clipping"></a>ガード バンド クリッピング


## <span id="ddk_guard_band_clipping_gg"></span><span id="DDK_GUARD_BAND_CLIPPING_GG"></span>


ドライバーが guard バンド クリッピングと GUID をフィールドをサポートしていることを通知\_で D3DExtendedCaps GUID [ **DdGetDriverInfo**](https://msdn.microsoft.com/library/windows/hardware/ff549404)します。 ガード バンドとは、ビューポート (および、レンダー ターゲットも) よりも大きい可能性のある四角形をどの頂点できますによってクリップする自動的にドライバー。 マイクロソフトの Direct3D クリッピングのコードは、ビューポートの代わりにこの四角形にクリップします。 バンド四角形が大きくなる可能性のガードを指定するドライバーを許可することでクリッピングのための新しい頂点を生成する必要が減少します。 1 つの例は 2047 を通じて-2048 範囲で画面の x 座標と y 座標が含まれている限り正しくレンダリングするハードウェア デバイスです。

Guard のバンドのクリッピングもメリットがアンチ エイリアスのハードウェアには、フィルター領域がレンダリング サーフェイスの範囲外に拡張できます。 これには、プリミティブがこの範囲にクリップされて幾何学的である場合に導入できるフィルターのエラーが削減されます。

適切な領域には、ドライバーにビューポート情報が渡されます。 これには、アプリケーションにクリップされ、ジオメトリに必要な実際のビューポートを指定します。 Guard のバンドのクリッピングを実装したくないドライバー作成者には、この情報を無視できます。 ドライバーがはさみをクリッピングまたは Direct3D のクリッピングを実行できるようにすることよりも遅くする可能性があるために、操作をマスクを実装するためにこのデータを使用しないことをお勧めします。

 

 





