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
ms.openlocfilehash: f8e07fae5c97429bb192cf2842f08e3fe72dce3d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338691"
---
# <a name="bgra-scan-out-support"></a>BGRA スキャン アウトのサポート


このセクションでは、Windows 7 およびそれ以降のオペレーティング システムにのみ適用されます。

DXGI、に対してスキャン アウト ビットがオン\_形式\_B8G8R8A8\_UNORM と DXGI\_形式\_B8G8R8A8\_UNORM\_SRGB 形式です。 そのため、ユーザー モードのディスプレイ ドライバーは、次の操作を実行できる必要があります。

-   これらの形式に含まれるプライマリのサーフェイスでのハンドル要求。

-   呼び出しを処理、 [ **SetDisplayMode** ](https://msdn.microsoft.com/library/windows/hardware/ff569535)はこれらの形式で作成したリソースの関数。

-   呼び出しを処理、 [ **PresentDXGI** ](https://msdn.microsoft.com/library/windows/hardware/ff569179)関数を両方のビット ブロック転送 (bitblt) を介してこれらの形式を表示し、操作を反転します。

-   呼び出しを処理、 [ **BltDXGI** ](https://msdn.microsoft.com/library/windows/hardware/ff538252) stretch、回転、を通じてこれらの形式をコピーする関数を解決するには (実際、RGBA バリアントの予想されるすべての bitblt 操作) にします。

 

 





