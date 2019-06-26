---
title: DirectX バージョンに関する通知
description: DirectX バージョンに関する通知
ms.assetid: 62c030cf-8eb6-4a94-bd15-730b9219291c
keywords:
- WDK DirectX 9.0 のバージョン番号
- DirectX バージョンの WDK DirectX 9.0 を通知します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08d9c5f7be466e5b130b8f056b4aeef3e9e396b3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372796"
---
# <a name="notifying-about-directx-version"></a>DirectX バージョンに関する通知


## <span id="ddk_notifying_about_directx_version_gg"></span><span id="DDK_NOTIFYING_ABOUT_DIRECTX_VERSION_GG"></span>


DirectX 8.0、およびそれ以降のドライバーが常に通知される、D3DGDI2 内のアプリケーションで使用されている DirectX のランタイム バージョン\_型\_DXVERSION 要求のバージョンについては、デバイスの機能をレポートすることができます。 さらに、アプリケーションでは、サーフェイスのピクセル形式をさまざまな操作を要求、ため、DirectX 9.0 と以降のドライバーが通知を受け取るも D3DGDI2 でアプリケーションをサポートする DirectX のランタイム バージョン\_型\_GETFORMATCOUNT と D3DGDI2\_型\_GETFORMAT クエリのため、それらのドライバーは、バージョンの操作を適切に処理できます。

例では、DirectX 9.0 またはそれ以降のドライバーは、DirectX のランタイムのバージョン 8.0 では、D3DMULTISAMPLE の要素を使用して、マルチ サンプリングされたサーフェイスでのサンプルの数を設定できます\_の種類、ドライバーがサポートするかどうかにかかわらず、型の列挙マスクのマルチ サンプリングします。 ただし、DirectX のランタイムのバージョン 9.0 は、DirectX 9.0 またはそれ以降のドライバーをする必要があります設定 D3DMULTISAMPLE\_、DDSCAPS3 型ビット\_マルチ サンプリング\_ドライバーとしてマスクのビットをサポートしていない限りをマスクするマスク。 D3DMULTISAMPLE の詳細については\_型、DirectX SDK のドキュメントを参照してください。

D3DGDI2\_型\_GETFORMATCOUNT クエリのランタイム バージョンのドライバーの通知を受け取る DirectX 9.0、 **dwReserved**のメンバー、 [ **DD\_GETFORMATCOUNTDATA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_dd_getformatcountdata)構造体。 **DwReserved** DD にメンバーが設定されている\_ランタイム\_バージョンについては、DirectX 9.0 の 0x00000900 であります。

D3DGDI2\_型\_GETFORMAT クエリのランタイム バージョンのドライバーの通知を受け取る DirectX 9.0、 **dwSize**で指定されている DDPIXELFORMAT 構造体のメンバー、**形式**のメンバー、 [ **DD\_GETFORMATDATA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_dd_getformatdata)構造体。 **DwSize** DD にメンバーを設定しても\_ランタイム\_バージョン。

 

 





