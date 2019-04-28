---
title: クロス プラットフォーム Direct3D ドライバーの開発
description: クロス プラットフォーム Direct3D ドライバーの開発
ms.assetid: 9363e0f9-4a58-4473-969f-eb54d0678632
keywords:
- クロス プラットフォーム開発の Direct3D WDK Windows 2000 の表示
- クロス プラットフォーム開発 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30f4b318399ffa6c6d89e69d569b50653c6e6423
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370772"
---
# <a name="cross-platform-direct3d-driver-development"></a>クロス プラットフォーム Direct3D ドライバーの開発


## <span id="ddk_cross_platform_direct3d_driver_development_gg"></span><span id="DDK_CROSS_PLATFORM_DIRECT3D_DRIVER_DEVELOPMENT_GG"></span>


Microsoft Windows 2000 以降および Windows 98/Me Direct3D DDI 型は、コンパイル時に直接的な互換性がない、相違点といくつかの種類の変更を各 DDI で構造体と関数のメンバーの名前付けのために入力します。 論理的にただし、同等メンバー DDI 種類ごとに同じ目的で機能します。

ポータブルの Windows 2000 以降と Windows 98、コードでは場合/Me を使用して*dx95type.h*、Windows Driver Kit (WDK) と前の Driver Development Kits (Ddk) に含まれているユーティリティ ファイル。 型の定義と Windows 98 間に発生するいくつかの名前付けの違いをマップするマクロが含まれています/Me、Windows 2000 と一般的なドライバーを有効にすると、以降のプラットフォームがそれらの間で使用するコードです。

 

 





