---
title: 全画面モードの動作
description: 全画面モードの動作
ms.assetid: 43e7fec0-4e4d-401c-80c7-3e0710313214
keywords:
- 全画面表示の回転 WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 468ebbc7574205809a59e973cce23b1f37d0fe5e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378054"
---
# <a name="full-screen-mode-behavior"></a>全画面モードの動作


ユーザー モードのディスプレイ ドライバーは、全画面表示モードでレンダリング デバイスが特定できます。

-   場合、**全画面表示**フラグのビット フィールドに設定されて、**フラグ**のメンバー、 [ **D3DDDIARG\_OPENRESOURCE** ](https://msdn.microsoft.com/library/windows/hardware/ff543232)構造体*pResource*ドライバーの呼び出しでパラメーターが指す[ **OpenResource** ](https://msdn.microsoft.com/library/windows/hardware/ff568611)関数。

-   場合、**プライマリ**フラグのビット フィールドに設定されて、**フラグ**のメンバー、 [ **D3DDDIARG\_CREATERESOURCE** ](https://msdn.microsoft.com/library/windows/hardware/ff542963)構造体*pResource*ドライバーの呼び出しでパラメーターが指す[ **CreateResource** ](https://msdn.microsoft.com/library/windows/hardware/ff540688)関数。

Microsoft DirectX 9.0 またはそれ以前に開発したアプリケーションをマイクロソフトの Direct3D のランタイムを呼び出すと、 *OpenResource* 、共有のプライマリ画面を開き、 *CreateResource*に追加のバック バッファーを作成します。 Microsoft DirectX 9 L アプリケーション、Direct3D のランタイムを呼び出すと、 *CreateResource* (呼び出さず*OpenResource*) すべてのバッファーをスワップ チェーンを作成します。 Direct3D のランタイムをプライマリ画面の向きを指定します、**回転**のメンバー、 [ **D3DDDIARG\_OPENRESOURCE** ](https://msdn.microsoft.com/library/windows/hardware/ff543232)と[**D3DDDIARG\_CREATERESOURCE** ](https://msdn.microsoft.com/library/windows/hardware/ff542963)構造を*pResource*両方の呼び出しでパラメーターが指す、 [ **OpenResource** ](https://msdn.microsoft.com/library/windows/hardware/ff568611)と[ **CreateResource** ](https://msdn.microsoft.com/library/windows/hardware/ff540688)関数、それぞれします。

ユーザー モードのディスプレイ ドライバーが回転したリソースをロックする必要があります全画面表示デバイスの場合に、回転のリソースにレンダリングし、回転したリソースからビット ブロック転送 (bitblt) を実行します。 (すべてのロック、bitblt、および表示する場合に移動する はこれらの中間レンダー ターゲット) 回転方向と横方向にプライマリの割り当てで通常は、ユーザー モードのディスプレイ ドライバーが中間レンダー ターゲットを作成します (は、印刷の向きをアナログ デジタル コンバーター \[DAC\]はアウト スキャンを使用して)。 ユーザー モードのディスプレイ ドライバーは、データを反転する呼び出されると、実行回転 bitblt 中間レンダー ターゲットからランドス ケープのバッファーを呼び出す前に、 [ **pfnPresentCb** ](https://msdn.microsoft.com/library/windows/hardware/ff568916)関数の問題をコマンドを反転します。

ユーザー モードのディスプレイ ドライバーは、回転のリソースと回転されていないリソースを含む bitblt 関数を実行する必要があります、たびに、Direct3D のランタイムを指定します、**回転**でフラグをビット フィールド、**フラグ**のメンバー[ **D3DDDIARG\_BLT** ](https://msdn.microsoft.com/library/windows/hardware/ff542884)ドライバーの呼び出しで構造[ **Blt** ](https://msdn.microsoft.com/library/windows/hardware/ff538251)関数に示すために、bitblt 関数の適切な回転を行う必要のあるドライバー。

DirectX 9 L アプリケーションは、つまり、すべてを正しい向きではレンダリングし、回転したバッファーにロックが正しく処理、回転対応であることができます。 ランタイムが、D3DDDI として、回転を常に指定する Direct3D のランタイムは、回転に対応したアプリケーションのスワップ チェーンを作成するとき\_回転\_で ID、**回転**のメンバー、 [**D3DDDIARG\_CREATERESOURCE** ](https://msdn.microsoft.com/library/windows/hardware/ff542963)ユーザー モードのディスプレイ ドライバーが回転に対応したアプリケーションが動作するため、特別な操作を実行する必要はないために構造体します。

 

 





