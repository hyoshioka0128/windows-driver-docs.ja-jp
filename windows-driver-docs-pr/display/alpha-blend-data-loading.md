---
title: アルファブレンドデータの読み込み
description: アルファブレンドデータの読み込み
ms.assetid: d61fbb07-a6b0-4623-bb5b-1c1218f570ae
keywords:
- alpha-blend データ読み込み (WDK DirectX VA)
- 画像のブレンド WDK DirectX VA、アルファブレンドデータ読み込み
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 820784ca57cc7cc98935251c971c06a22c9aec30
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839072"
---
# <a name="alpha-blend-data-loading"></a>アルファブレンドデータの読み込み


## <span id="ddk_alpha_blend_data_loading_gg"></span><span id="DDK_ALPHA_BLEND_DATA_LOADING_GG"></span>


[BDXVA\_Func 変数](bdxva-func-variable.md)が2に等しい場合、指定された操作は、ビデオデータとブレンドするアルファブレンドサーフェイスを指定するデータの読み込みです。 アルファブレンディングデータを読み込むには、次の3つの方法があります。

-   インデックスアルファ 4-4 (IA44) またはアルファインデックス 4-4 (AI44) のアルファブレンドサーフェイスを持つ16エントリ AYUV パレット

-   $ Entry AYUV パレットと、使用可能なデータの選択

-   AYUV グラフィック画面

[**DXVA\_ConfigAlphaLoad**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configalphaload)構造体は、これらのメソッドのうちどれを使用するかを決定します。

 

 





