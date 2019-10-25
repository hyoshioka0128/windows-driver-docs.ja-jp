---
title: 2 次元の操作のサポート
description: 2 次元の操作のサポート
ms.assetid: 09611bba-5b36-4b7d-8d93-a99590eb5bbe
keywords:
- 2次元操作 (WDK DirectX 9.0)
- 2D 操作 WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c432e018a9b0238f7c2282f763971b7838d369c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829390"
---
# <a name="supporting-two-dimensional-operations"></a>2 次元の操作のサポート


## <span id="ddk_supporting_two_dimensional_operations_gg"></span><span id="DDK_SUPPORTING_TWO_DIMENSIONAL_OPERATIONS_GG"></span>


DirectX 9.0 ランタイムは、ランタイムが検出したドライバーのバージョンに応じて、2次元 (2D) のピクセルコピー操作を実行するようにドライバーに指示します。 DirectX 8.1 以前のドライバーの場合、ランタイムはドライバーの[*Ddblt*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_blt)関数を呼び出し、この呼び出しを[コマンドストリーム](command-stream.md)と同期します。 DirectX 9.0 以降のドライバーでは、ランタイムは D3DDP2OP\_BLT、D3DDP2OP\_SURFACEBLT、または D3DDP2OP\_COLORFILL 操作コードと共に[**D3DHAL\_DP2BLT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2blt)、 [**D3DHAL\_DP2SURFACEBLT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2surfaceblt)を[**渡します。D3DHAL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2colorfill)は、それぞれコマンドストリームで\_を DP2COLORFILL 構造体にします。 DirectX 9.0 以降のドライバーは、これらの2D 操作コードをサポートする必要があります。

ランタイムが、DirectX 8.1 以前のドライバーの*ddblt*関数の呼び出しで ddblt\_colorfill フラグを指定した場合、ランタイムはターゲットサーフェスを認識している限り、D3DCOLOR fill-color 型を明示的なピクセル値に変換します。形式 (つまり、形式のコードは、D3DFORMAT 列挙型のコードの1つです)。 形式がベンダーによって提供され、ランタイムによって認識されない場合、ランタイムは D3DCOLOR fill color 型を直接ドライバーに渡して処理します。 ただし、ランタイムは、DirectShow によって使用される特定の色形式の D3DCOLOR の塗りつぶし色の種類を明示的なピクセル値に変換しますが、それ以外の場合はドライバーに対してプライベートです。

 

 





