---
title: マルチサンプリングの制御
description: マルチサンプリングの制御
ms.assetid: 73cdfda8-f67a-470b-a17e-0bf78a5d1df1
keywords:
- レンダリングの DirectX 8.0 リリース ノート WDK Windows 2000 表示、マルチ サンプリングに制御します。
- マルチ サンプリングのレンダリングを制御する WDK DirectX 8.0 では、
- WDK DirectX multisamples 8.0 では、制御のレンダリング
- D3DRS_MULTISAMPLEANTIALIAS
- D3DRS_MULTISAMPLEMASK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 545ad75a6ef2a188fb48fda65cd27daa731bdd71
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572710"
---
# <a name="controlling-multisampling"></a>マルチサンプリングの制御


## <span id="ddk_controlling_multisampling_gg"></span><span id="DDK_CONTROLLING_MULTISAMPLING_GG"></span>


2 つは、D3DRENDERSTATETYPE 列挙コントロールのマルチ サンプリング レンダリングの状態をレンダリングします。 D3DRENDERSTATETYPE の詳細については、DirectX 8.0 SDK ドキュメントを参照してください。

### <a name="span-idd3drsmultisampleantialiasspanspan-idd3drsmultisampleantialiasspand3drsmultisampleantialias"></a><span id="d3drs_multisampleantialias"></span><span id="D3DRS_MULTISAMPLEANTIALIAS"></span>D3DRS\_MULTISAMPLEANTIALIAS

マルチ サンプリングのレンダー ターゲットのバッファーを使用する場合、どのように個々 のサンプルを決定するブール値が計算されます。 設定すると**TRUE**、複数のサンプルが全シーン アンチエイリアシングがそれぞれ別のサンプルの位置にある複数のサンプルをサンプリングすることによって実行されるように計算されます。 設定すると**FALSE**、複数のサンプルはすべて、同じサンプル値 (ピクセルの中心でサンプリング) であり multisample バッファーに nonantialiased レンダリングで記述します。 1 つのサンプルのバッファーを表示するときに、このレンダリング状態を指定しても効果はありません。 既定値は**TRUE**します。

### <a name="span-idd3drsmultisamplemaskspanspan-idd3drsmultisamplemaskspand3drsmultisamplemask"></a><span id="d3drs_multisamplemask"></span><span id="D3DRS_MULTISAMPLEMASK"></span>D3DRS\_MULTISAMPLEMASK

このマスクは、LSB から始まる、各ビット レンダー ターゲットをマルチ サンプル、サンプルの 1 つの変更を制御します。 したがって、8 サンプル レンダー ターゲットでは、下位バイトが含まれます 8 書き込み可能には各 8 のサンプルの。 1 つのサンプルのバッファーを表示するときに、このレンダリング状態を指定しても効果はありません。 既定値は、0 xffffffff です。

このレンダリング状態では、各パスがサンプルのサブセットを更新する場所のジオメトリのマルチパス レンダリングを行って、集積/離散バッファーとして multisample バッファーの使用を有効します。

マルチ サンプリングのレンダー ターゲットでは、各サンプルでは、最終的な表示されるイメージに統一された強度を提供します。 たとえば、マルチ サンプリング モードは、3、マルチ サンプリングのマスクを使用して有効になっているサンプルの数は 2 に検討してください。 したがって、描画された画像の結果として得られる強さは、2/3 です。 つまり、2/3 でのすべてのピクセルの各赤、緑、および青のコンポーネントの強度が考慮されます。

 

 





