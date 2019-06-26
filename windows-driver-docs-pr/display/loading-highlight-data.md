---
title: ハイライト データの読み込み
description: ハイライト データの読み込み
ms.assetid: d893fdbe-847d-45a7-b2b2-62da505c8aeb
keywords:
- データ読み込みの WDK DirectX VA をアルファ ブレンド
- ブレンド画像 WDK DirectX va なので、アルファ ブレンドのデータの読み込み
- WDK DirectX VA 四角形の領域を強調表示されます。
- 四角形領域 WDK DirectX VA を強調表示されます。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0e3b7cbf93d1a1bc85c7d9d0582e2ca069ff1e9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360901"
---
# <a name="loading-highlight-data"></a>ハイライト データの読み込み


## <span id="ddk_loading_highlight_data_gg"></span><span id="DDK_LOADING_HIGHLIGHT_DATA_GG"></span>


[ **DXVA\_を強調表示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_highlight)構造体は、サブピクチャの四角形の領域を強調表示されているを指定し、DCCMD データ バックアップおよび DPXD 画面と共に、アルファ ブレンドの画面を作成するために使用します。 強調表示のデータは、DVD-ROM 仕様と互換性のある方法で書式設定されます。 DVD サブピクチャ定義およびデータ フィールドの解釈の詳細な説明を参照してください。*読み取り専用のディスク、DVD 仕様。パート 3 - ビデオの仕様 (v します。1.11、1999 年 5 月)* します。

 

 





