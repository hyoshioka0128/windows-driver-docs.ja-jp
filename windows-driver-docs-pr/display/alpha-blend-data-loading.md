---
title: アルファ ブレンド データの読み込み
description: アルファ ブレンド データの読み込み
ms.assetid: d61fbb07-a6b0-4623-bb5b-1c1218f570ae
keywords:
- データ読み込みの WDK DirectX VA をアルファ ブレンド
- ブレンド画像 WDK DirectX va なので、アルファ ブレンドのデータの読み込み
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5edf23d4319372fb9f76f989504c7571dea57250
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344639"
---
# <a name="alpha-blend-data-loading"></a>アルファ ブレンド データの読み込み


## <span id="ddk_alpha_blend_data_loading_gg"></span><span id="DDK_ALPHA_BLEND_DATA_LOADING_GG"></span>


ときに、 [bDXVA\_Func 変数](bdxva-func-variable.md)は 2 と等しい、指定された操作がビデオ データと統合するアルファ ブレンドの画面を指定するデータの読み込み。 アルファ ブレンドのデータを読み込むことがある 3 つの方法があります。

-   16 エントリ AYUV パレット インデックス アルファ 4-4 と (IA44) またはアルファ インデックス 4-4 (AI44) 画面のアルファ ブレンド

-   DPXD、強調表示、および DCCMD データを 16 エントリ AYUV パレット

-   AYUV のグラフィック画面

[ **DXVA\_ConfigAlphaLoad** ](https://msdn.microsoft.com/library/windows/hardware/ff563129)構造体を使用するどちらの方法を決定します。

 

 





