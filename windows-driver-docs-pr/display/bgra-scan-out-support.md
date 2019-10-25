---
title: BGRA Scan Out のサポート
description: BGRA Scan Out のサポート
ms.assetid: 88ef5de7-59cc-4a8a-aaf7-74489a7ac0ab
keywords:
- Direct3D バージョン 10.1 WDK Windows 7 display、BGRA scan out サポート
- BGRA scan out サポート (WDK Windows 7 ディスプレイ)
- スキャンアウトサポート WDK Windows 7 ディスプレイ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f96d95af52ab090d3625a65822b3d7967cb819c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839069"
---
# <a name="bgra-scan-out-support"></a>BGRA Scan Out のサポート


このセクションは、Windows 7 以降のオペレーティングシステムにのみ適用されます。

スキャンアウトビットは、DXGI\_形式\_B8G8R8A8\_UNORM および DXGI\_形式\_B8G8R8A8\_UNORM\_SRGB 形式に対して有効になっています。 そのため、ユーザーモードの表示ドライバーでは、次の操作を実行できる必要があります。

-   これらの形式のプライマリサーフェイスの要求を処理します。

-   これらの形式で作成されたリソースに対する[**Setdisplaymode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_setdisplaymode)関数の呼び出しを処理します。

-   ビットブロック転送 (bitblt) とフリップ操作の両方によってこれらの形式を提示するために、 [**present**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)関数の呼び出しを処理します。

-   [**Bltdxgi**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)関数への呼び出しを処理して、これらの形式を伸縮、ローテーション、および解決することによって、これらの形式をコピーします (実際には、RGBA バリアントで想定されているすべての bitblt 操作)。

 

 





