---
title: ビデオ処理用のレンダー ターゲット サーフェスの作成
description: ビデオ処理用のレンダー ターゲット サーフェスの作成
ms.assetid: f18b348d-837a-4e1b-b91a-40593661bd56
keywords:
- WDK DirectX va なので、ビデオの処理対象のサーフェスをレンダリングします。
- レンダリング ターゲット サーフェス WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f8c3226e5f6c621ebfeaad5c0b65624b2df8f69
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370234"
---
# <a name="creating-a-render-target-surface-for-video-processing"></a>ビデオ処理用のレンダー ターゲット サーフェスの作成


マイクロソフトの Direct3D ランタイムが呼び出すユーザー モードのディスプレイ ドライバーの[ **CreateResource** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)関数を作成するビデオの処理のターゲットのサーフェスをレンダリングします。 ユーザー モードのディスプレイ ドライバーが処理の有無によるビデオのレンダー ターゲットの画面を作成することを決定します、 **VideoProcessRenderTarget**でフラグをビット フィールド、**フラグ**のメンバー、[ **D3DDDIARG\_CREATERESOURCE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)構造体、 *pResource*パラメーターの**CreateResource**ポインター。 ユーザー モードのディスプレイ ドライバーは、ビデオの処理のため、必ずしも 3-D のこのレンダー ターゲットを使用できます。 ユーザー モードのディスプレイ ドライバーは、通常の RGB 3-D レンダリング ターゲットのサーフェスにビデオ処理を実行できます。 ただし、ユーザー モードのディスプレイ ドライバーでは、3-D のハードウェアがレンダー ターゲットとしてサポート YUV 形式に出力できる多くの場合。

以下は、ドライバーは、ビデオの処理の有効なレンダー ターゲットとしてサポートする必要がありますのみサーフェスの種類です。

-   作成された RGB または YUV サーフェス、 **VideoProcessRenderTarget**フラグのビット フィールド。

-   作成された RGB サーフェス、**レンダリング ターゲット**フラグのビット フィールド。

-   作成された RGB テクスチャ、**レンダリング ターゲット**と**テクスチャ**フラグのビット フィールド。

 

 





