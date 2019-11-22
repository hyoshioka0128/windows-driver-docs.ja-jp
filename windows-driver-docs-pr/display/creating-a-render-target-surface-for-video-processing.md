---
title: ビデオ処理用のレンダー ターゲット サーフェスの作成
description: ビデオ処理用のレンダー ターゲット サーフェスの作成
ms.assetid: f18b348d-837a-4e1b-b91a-40593661bd56
keywords:
- ビデオ処理 WDK DirectX VA、レンダーターゲットサーフェス
- ターゲットサーフェスのレンダリング WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90924f7b350884d85140d903214dd59b766bec0d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839031"
---
# <a name="creating-a-render-target-surface-for-video-processing"></a>ビデオ処理用のレンダー ターゲット サーフェスの作成


Microsoft Direct3D ランタイムは、ビデオ処理のレンダーターゲットサーフェイスを作成するために、ユーザーモードの display driver の[**Createresource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)関数を呼び出します。 ユーザーモードの表示ドライバーは、 **createresource**の*presource*パラメーターが指す[**D3DDDIARG\_Createresource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)構造体の**Flags**メンバーに、 **VideoProcessRenderTarget**ビットフィールドフラグがあるかどうかを確認するためのレンダリングターゲットサーフェイスを作成する必要があると判断します。 ユーザーモード表示ドライバーは、このレンダーターゲットをビデオ処理に使用できますが、必ずしも3-d では使用できません。 ユーザーモード表示ドライバーでは、通常の RGB 3-d レンダーターゲットサーフェイスでビデオ処理を実行できます。 ただし、多くの場合、ユーザーモード表示ドライバーは、3-d ハードウェアがレンダーターゲットとしてサポートできない YUV 形式に出力できます。

次に示すのは、ドライバーがビデオ処理の有効なレンダーターゲットとしてサポートする必要がある表面の種類のみです。

-   **VideoProcessRenderTarget**ビットフィールドフラグを使用して作成された RGB または YUV サーフェイス。

-   **作り**ビットフィールドフラグを使用して作成された RGB サーフェイス。

-   **作り**と**テクスチャ**のビットフィールドフラグを使用して作成された RGB テクスチャ。

 

 





