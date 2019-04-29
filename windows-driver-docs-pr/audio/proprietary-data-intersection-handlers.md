---
title: 独自のデータ交差ハンドラー
description: 独自のデータ交差ハンドラー
ms.assetid: 8ed497d3-2344-4979-9859-e66a4713e6c5
keywords:
- 交差部分のデータ ハンドラー WDK オーディオ、専用
- 独自のデータの積集合ハンドラー WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 20503c2ac74e39556e569c0d2023c9d457c8708c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328734"
---
# <a name="proprietary-data-intersection-handlers"></a>独自のデータ交差ハンドラー


## <span id="proprietary_data_intersection_handlers"></span><span id="PROPRIETARY_DATA_INTERSECTION_HANDLERS"></span>


アダプターの独自のハンドラーを記述することで、既定の交差部分のデータ ハンドラーの制限を克服できます。 として独自のハンドラーが実装されている、 [ **IMiniport::DataRangeIntersection** ](https://msdn.microsoft.com/library/windows/hardware/ff536764)ミニポート ドライバー オブジェクトのメソッド。 サンプル アダプターのドライバーの例については Microsoft Windows Driver Kit (WDK) でを参照してください。 **DataRangeIntersection**メソッド。

非標準のハードウェア機能で適切に指定することはできませんを補うことができます独自のデータの積集合ハンドラー、 [ **KSDATARANGE\_オーディオ**](https://msdn.microsoft.com/library/windows/hardware/ff537096)構造体。 たとえば、WDK で AC97 サンプル アダプターのドライバーは、ハードウェアを再生中、2 つ以上のオーディオ チャンネルをサポートすることができますが、mono をサポートすることはできませんを管理します。 サンプルの[ **DataRangeIntersection** ](https://msdn.microsoft.com/library/windows/hardware/ff536764)メソッドは、他のフィルターのソースの暗証番号 (pin) のデータ範囲は mono に制限されて かどうかを判断します (つまり、 **MaximumChannels** &lt; 2)。 かどうか、そのため、失敗、呼び出しの状態を返すことによって\_いいえ\_一致します。

独自のデータの積集合のハンドラーでは、他のピンでデータの交差部分を処理するためにそのピンのいくつかのデータの交差部分を処理し、ポート ドライバーの既定の交差部分のデータ ハンドラーを許可することのオプションがあります。

このセクションの残りの部分では、独自のデータの積集合のハンドラーを実装するためのガイドラインを示します。

 

 




