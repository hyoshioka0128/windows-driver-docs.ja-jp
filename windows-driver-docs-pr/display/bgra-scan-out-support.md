---
title: BGRA スキャン アウトのサポート
description: BGRA スキャン アウトのサポート
ms.assetid: 88ef5de7-59cc-4a8a-aaf7-74489a7ac0ab
keywords:
- Direct3D バージョン 10.1 WDK Windows 7 の表示、BGRA スキャン アウトのサポート
- BGRA スキャン アウト サポート Windows 7 の WDK の表示
- スキャン アウト サポート Windows 7 の WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17e2bb0b87036ca5023220559f7c23bc6f43cfb9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384627"
---
# <a name="bgra-scan-out-support"></a>BGRA スキャン アウトのサポート


このセクションでは、Windows 7 およびそれ以降のオペレーティング システムにのみ適用されます。

DXGI、に対してスキャン アウト ビットがオン\_形式\_B8G8R8A8\_UNORM と DXGI\_形式\_B8G8R8A8\_UNORM\_SRGB 形式です。 そのため、ユーザー モードのディスプレイ ドライバーは、次の操作を実行できる必要があります。

-   これらの形式に含まれるプライマリのサーフェイスでのハンドル要求。

-   呼び出しを処理、 [ **SetDisplayMode** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_setdisplaymode)はこれらの形式で作成したリソースの関数。

-   呼び出しを処理、 [ **PresentDXGI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)関数を両方のビット ブロック転送 (bitblt) を介してこれらの形式を表示し、操作を反転します。

-   呼び出しを処理、 [ **BltDXGI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions) stretch、回転、を通じてこれらの形式をコピーする関数を解決するには (実際、RGBA バリアントの予想されるすべての bitblt 操作) にします。

 

 





