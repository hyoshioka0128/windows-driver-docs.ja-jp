---
title: ビデオ処理用のレンダー ターゲット サーフェスの作成
description: ビデオ処理用のレンダー ターゲット サーフェスの作成
ms.assetid: f18b348d-837a-4e1b-b91a-40593661bd56
keywords:
- WDK DirectX va なので、ビデオの処理対象のサーフェスをレンダリングします。
- レンダリング ターゲット サーフェス WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8680bff61779b8bfe5331e29a1698cabbb1eb566
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346907"
---
# <a name="creating-a-render-target-surface-for-video-processing"></a>ビデオ処理用のレンダー ターゲット サーフェスの作成


マイクロソフトの Direct3D ランタイムが呼び出すユーザー モードのディスプレイ ドライバーの[ **CreateResource** ](https://msdn.microsoft.com/library/windows/hardware/ff540688)関数を作成するビデオの処理のターゲットのサーフェスをレンダリングします。 ユーザー モードのディスプレイ ドライバーが処理の有無によるビデオのレンダー ターゲットの画面を作成することを決定します、 **VideoProcessRenderTarget**でフラグをビット フィールド、**フラグ**のメンバー、[ **D3DDDIARG\_CREATERESOURCE** ](https://msdn.microsoft.com/library/windows/hardware/ff542963)構造体、 *pResource*パラメーターの**CreateResource**ポインター。 ユーザー モードのディスプレイ ドライバーは、ビデオの処理のため、必ずしも 3-D のこのレンダー ターゲットを使用できます。 ユーザー モードのディスプレイ ドライバーは、通常の RGB 3-D レンダリング ターゲットのサーフェスにビデオ処理を実行できます。 ただし、ユーザー モードのディスプレイ ドライバーでは、3-D のハードウェアがレンダー ターゲットとしてサポート YUV 形式に出力できる多くの場合。

以下は、ドライバーは、ビデオの処理の有効なレンダー ターゲットとしてサポートする必要がありますのみサーフェスの種類です。

-   作成された RGB または YUV サーフェス、 **VideoProcessRenderTarget**フラグのビット フィールド。

-   作成された RGB サーフェス、**レンダリング ターゲット**フラグのビット フィールド。

-   作成された RGB テクスチャ、**レンダリング ターゲット**と**テクスチャ**フラグのビット フィールド。

 

 





