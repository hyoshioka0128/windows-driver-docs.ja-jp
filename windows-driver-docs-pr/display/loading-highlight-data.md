---
title: ハイライト データの読み込み
description: ハイライト データの読み込み
ms.assetid: d893fdbe-847d-45a7-b2b2-62da505c8aeb
keywords:
- alpha-blend データ読み込み (WDK DirectX VA)
- 画像のブレンド WDK DirectX VA、アルファブレンドデータ読み込み
- 強調表示された四角形領域 WDK DirectX VA
- 四角形の強調表示された領域 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5dfcd051eb8794c2ee82d6c1cf5e6dd12392d70
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840601"
---
# <a name="loading-highlight-data"></a>ハイライト データの読み込み


## <span id="ddk_loading_highlight_data_gg"></span><span id="DDK_LOADING_HIGHLIGHT_DATA_GG"></span>


[**DXVA\_強調表示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_highlight)構造体は、サブピクチャの強調表示された四角形領域を指定し、dccmd データと共に使用されます。また、アルファブレンドサーフェイスを作成するには、[] を選択します。 強調表示データは、DVD ROM 仕様と互換性のある方法で書式設定されます。 DVD のサブピクチャ定義とデータフィールドの解釈の詳細については、「*読み取り専用ディスクの Dvd 仕様: パート 3-ビデオ仕様 (1.11、5月 1999)* 」を参照してください。

 

 





