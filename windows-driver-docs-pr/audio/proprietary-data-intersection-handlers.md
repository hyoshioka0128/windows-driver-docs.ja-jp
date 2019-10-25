---
title: 独自のデータ交差ハンドラー
description: 独自のデータ交差ハンドラー
ms.assetid: 8ed497d3-2344-4979-9859-e66a4713e6c5
keywords:
- データ交差ハンドラー WDK オーディオ、専有
- 専有データ-交差ハンドラー WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e4ad0a7ee592021c06ce44480b8c4a95bf3b125
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830223"
---
# <a name="proprietary-data-intersection-handlers"></a>独自のデータ交差ハンドラー


## <span id="proprietary_data_intersection_handlers"></span><span id="PROPRIETARY_DATA_INTERSECTION_HANDLERS"></span>


アダプターの独自のハンドラーを記述することで、既定のデータの共通部分ハンドラーの制限を克服できます。 独自のハンドラーは、ミニポートドライバーオブジェクトの[**IMiniport::D ataRangeIntersection 集合**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiport-datarangeintersection)メソッドとして実装されます。 **Datarangeintersection**という方法の例については、Microsoft Windows Driver KIT (WDK) のアダプタードライバーのサンプルを参照してください。

独自のデータ積集合ハンドラーは、 [**Ksk datarの\_AUDIO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_audio)構造体で適切に指定できない非標準のハードウェア機能を補正できます。 たとえば、WDK の AC97 サンプルアダプタードライバーは、再生中に2つ以上のオーディオチャネルをサポートできるハードウェアを管理しますが、mono はサポートしていません。 このサンプルの[**Datarangeintersection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiport-datarangeintersection)メソッドは、他のフィルターのソースピンのデータ範囲が mono に限定されているかどうかを判断します (つまり、 **maximumchannels** &lt; 2)。 含まれている場合は、STATUS\_\_一致しない状態を返すことで、呼び出しが失敗します。

独自のデータ積集合ハンドラーには、一部のピンのデータ交差部分を処理するオプションがあり、ポートドライバーの既定のデータの交差ハンドラーが他の pin のデータ交差を処理できるようにします。

このセクションの残りの部分では、独自のデータ共通部分ハンドラーを実装するためのガイドラインを示します。

 

 




