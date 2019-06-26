---
title: 全画面モードの動作
description: 全画面モードの動作
ms.assetid: 43e7fec0-4e4d-401c-80c7-3e0710313214
keywords:
- 全画面表示の回転 WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84ba8a6d3c42648501cfa28cff7ee93d0a9cdda3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356365"
---
# <a name="full-screen-mode-behavior"></a>全画面モードの動作


ユーザー モードのディスプレイ ドライバーは、全画面表示モードでレンダリング デバイスが特定できます。

-   場合、**全画面表示**フラグのビット フィールドに設定されて、**フラグ**のメンバー、 [ **D3DDDIARG\_OPENRESOURCE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_openresource)構造体*pResource*ドライバーの呼び出しでパラメーターが指す[ **OpenResource** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_openresource)関数。

-   場合、**プライマリ**フラグのビット フィールドに設定されて、**フラグ**のメンバー、 [ **D3DDDIARG\_CREATERESOURCE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)構造体*pResource*ドライバーの呼び出しでパラメーターが指す[ **CreateResource** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)関数。

Microsoft DirectX 9.0 またはそれ以前に開発したアプリケーションをマイクロソフトの Direct3D のランタイムを呼び出すと、 *OpenResource* 、共有のプライマリ画面を開き、 *CreateResource*に追加のバック バッファーを作成します。 Microsoft DirectX 9 L アプリケーション、Direct3D のランタイムを呼び出すと、 *CreateResource* (呼び出さず*OpenResource*) すべてのバッファーをスワップ チェーンを作成します。 Direct3D のランタイムをプライマリ画面の向きを指定します、**回転**のメンバー、 [ **D3DDDIARG\_OPENRESOURCE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_openresource)と[**D3DDDIARG\_CREATERESOURCE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)構造を*pResource*両方の呼び出しでパラメーターが指す、 [ **OpenResource** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_openresource)と[ **CreateResource** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)関数、それぞれします。

ユーザー モードのディスプレイ ドライバーが回転したリソースをロックする必要があります全画面表示デバイスの場合に、回転のリソースにレンダリングし、回転したリソースからビット ブロック転送 (bitblt) を実行します。 (すべてのロック、bitblt、および表示する場合に移動する はこれらの中間レンダー ターゲット) 回転方向と横方向にプライマリの割り当てで通常は、ユーザー モードのディスプレイ ドライバーが中間レンダー ターゲットを作成します (は、印刷の向きをアナログ デジタル コンバーター \[DAC\]はアウト スキャンを使用して)。 ユーザー モードのディスプレイ ドライバーは、データを反転する呼び出されると、実行回転 bitblt 中間レンダー ターゲットからランドス ケープのバッファーを呼び出す前に、 [ **pfnPresentCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_presentcb)関数の問題をコマンドを反転します。

ユーザー モードのディスプレイ ドライバーは、回転のリソースと回転されていないリソースを含む bitblt 関数を実行する必要があります、たびに、Direct3D のランタイムを指定します、**回転**でフラグをビット フィールド、**フラグ**のメンバー[ **D3DDDIARG\_BLT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_blt)ドライバーの呼び出しで構造[ **Blt** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_blt)関数に示すために、bitblt 関数の適切な回転を行う必要のあるドライバー。

DirectX 9 L アプリケーションは、つまり、すべてを正しい向きではレンダリングし、回転したバッファーにロックが正しく処理、回転対応であることができます。 ランタイムが、D3DDDI として、回転を常に指定する Direct3D のランタイムは、回転に対応したアプリケーションのスワップ チェーンを作成するとき\_回転\_で ID、**回転**のメンバー、 [**D3DDDIARG\_CREATERESOURCE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)ユーザー モードのディスプレイ ドライバーが回転に対応したアプリケーションが動作するため、特別な操作を実行する必要はないために構造体します。

 

 





