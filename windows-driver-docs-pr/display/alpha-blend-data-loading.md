---
title: アルファ ブレンド データの読み込み
description: アルファ ブレンド データの読み込み
ms.assetid: d61fbb07-a6b0-4623-bb5b-1c1218f570ae
keywords:
- データ読み込みの WDK DirectX VA をアルファ ブレンド
- ブレンド画像 WDK DirectX va なので、アルファ ブレンドのデータの読み込み
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fccf18e298e57e79a4027f5503247d3c719e3489
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384638"
---
# <a name="alpha-blend-data-loading"></a>アルファ ブレンド データの読み込み


## <span id="ddk_alpha_blend_data_loading_gg"></span><span id="DDK_ALPHA_BLEND_DATA_LOADING_GG"></span>


ときに、 [bDXVA\_Func 変数](bdxva-func-variable.md)は 2 と等しい、指定された操作がビデオ データと統合するアルファ ブレンドの画面を指定するデータの読み込み。 アルファ ブレンドのデータを読み込むことがある 3 つの方法があります。

-   16 エントリ AYUV パレット インデックス アルファ 4-4 と (IA44) またはアルファ インデックス 4-4 (AI44) 画面のアルファ ブレンド

-   DPXD、強調表示、および DCCMD データを 16 エントリ AYUV パレット

-   AYUV のグラフィック画面

[ **DXVA\_ConfigAlphaLoad** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_configalphaload)構造体を使用するどちらの方法を決定します。

 

 





