---
title: 下位レベルの MIP マップ テクスチャを生成します。
description: 下位レベルの MIP マップ テクスチャを生成します。
ms.assetid: fbfb0d1b-468d-4e7f-865e-bdc7d19f5516
keywords:
- MIP マップ テクスチャ WDK DirectX 9.0、サブレベルの生成
- MIP マップ テクスチャ WDK DirectX 9.0 のサブレベル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d51be4c4595834d7d458c3ec9ca57f8735b0988
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527455"
---
# <a name="generating-sublevels-of-mip-map-textures"></a>下位レベルの MIP マップ テクスチャを生成します。


## <span id="ddk_generating_sublevels_of_mip_map_textures_gg"></span><span id="DDK_GENERATING_SUBLEVELS_OF_MIP_MAP_TEXTURES_GG"></span>


ディスプレイ ドライバーがサポートするには、DDCAPS2 MIP マップ テクスチャのサブレベルを自動的に生成するを示します\_CANAUTOGENMIPMAP ビット、 **dwCaps2**のメンバー、 [ **DDCORECAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff549248)構造体。 ドライバーでは、この DDCORECAPS 構造を指定します、 **ddCaps**のメンバー、 [ **DD\_HALINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff551627)構造体。 DD\_HALINFO がドライバーのによって返される[ **DrvGetDirectDrawInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff556229)関数。 ディスプレイ ドライバーが、D3DFORMAT を設定して、特定の形式を画面が自動的に生成する下位レベルをサポートして かどうかを示すも\_OP\_AUTOGENMIPMAP フラグ、 **dwOperations**のメンバー、[ **DDPIXELFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff550274)形式については、構造体。

テクスチャ サーフェスを作成すると、Direct3D のランタイム設定、DDSCAPS3\_AUTOGENMIPMAP ビット、 **dwCaps3** 、DDSCAPSEX のメンバー ([**DDSCAPS2**](https://msdn.microsoft.com/library/windows/hardware/ff550292))構造体のこのテクスチャの MIP マップ サブレベルが自動的に生成されることを示します。 Direct3D では、一部のテクスチャの MIP マップ サブレベルを自動的に生成して自動的に生成するいくつかのテクスチャを指示する場合、ドライバー blit 操作にのみ実行できます (D3DDP2OP\_TEXBLT) で、次の説明に従って、これらのテクスチャでシナリオ:

-   ドライバーでは、自動的に生成するにはない変換先のテクスチャの MIP マップをソース テクスチャからブリットことはできません。

-   場合は自動的に生成しない MIP ソース テクスチャからドライバー ブリットでは、一致する最上位のレベルがドライバーのみブリットは、移行先テクスチャにマップされます。 ソース テクスチャからサブレベルは無視されます。 下位レベルの変換先を生成できます。

-   同様に、変換先のテクスチャを両方の自動生成 MIP をソースからドライバー ブリットがマップされている場合、最上位のドライバーのみブリットはレベルを照合します。 ソース テクスチャからサブレベルは無視されます。 下位レベルの変換先を生成できます。

ドライバーが、D3DDP2OP を受信する下位レベルの MIP マップ テクスチャを生成する\_GENERATEMIPSUBLEVELS がコマンドと共に、 [ **D3DHAL\_DP2GENERATEMIPSUBLEVELS** ](https://msdn.microsoft.com/library/windows/hardware/ff545570)構造体。 このコマンドを受信するために、テクスチャのサーフェイスの形式が、D3DFORMAT を公開する必要があります\_OP\_AUTOGENMIPMAP フラグ。

[ドライバー-マネージ リソース](driver-managed-resources.md)ドライバーの削除や、ビデオ メモリ内のリソースを置換ドライバーする必要がありますを使用して、最後のセットのフィルターの種類をサブレベルを自動的に生成する場合。 Direct3D が、D3DDP2OP を送信しないため、Direct3D には、削除と、リソースの交換は制御しません、\_ドライバーに GENERATEMIPSUBLEVELS コマンド。

Direct3D のランタイムは、ドライバーを呼び出すことはできません[ *DdLock* ](https://msdn.microsoft.com/library/windows/hardware/ff549599)関数またはその他を使用して、 [DDI](direct3d-driver-ddi.md)自動生成された MIP マップ テクスチャの下位レベルにアクセスします。 これは、ことを示しますなど、軽量の MIP マップ テクスチャの MIP マップ自動生成されたテクスチャの下位レベルは「暗黙」として適切なドライバーによって指定できます。 ドライバーは、「完了」surface データ構造を指定する必要はありません。 ただし、Direct3D は、ドライバーの呼び出すできる必要があります、 *DdLock*または[ *DdBlt* ](https://msdn.microsoft.com/library/windows/hardware/ff549205)関数では、送信、D3DDP2OP\_BLT コマンド、または (他の任意の DDI の使用[ドライバー管理のテクスチャ](driver-managed-textures.md)、動的テクスチャまたはベンダー固有の形式のみ)、自動生成された MIP マップ テクスチャの最上位レベルにアクセスします。

 

 





