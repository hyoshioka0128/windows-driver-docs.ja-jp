---
title: DirectX バージョンに関する通知
description: DirectX バージョンに関する通知
ms.assetid: 62c030cf-8eb6-4a94-bd15-730b9219291c
keywords:
- バージョン番号 WDK DirectX 9.0
- DirectX バージョンに関する通知 WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a77e920b79746aec760ea8ed0e157b742034d8c3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840526"
---
# <a name="notifying-about-directx-version"></a>DirectX バージョンに関する通知


## <span id="ddk_notifying_about_directx_version_gg"></span><span id="DDK_NOTIFYING_ABOUT_DIRECTX_VERSION_GG"></span>


DirectX 8.0 以降のドライバーは、D3DGDI2\_TYPE\_DXVERSION 要求でアプリケーションによって使用されている DirectX ランタイムバージョンについて常に通知されるため、バージョンのデバイス機能を報告できます。 さらに、アプリケーションはさまざまなピクセル形式でサーフェイスに対する操作を要求するので、D3DGDI2\_TYPE\_GETFORMATCOUNT でアプリケーションがサポートしている DirectX ランタイムのバージョンについても、DirectX 9.0 以降のドライバーについて通知されます。また、D3DGDI2 は\_\_入力して、これらのドライバーがバージョンの操作を適切に処理できるようにします。

たとえば、DirectX ランタイムのバージョン8.0 では、DirectX 9.0 以降のドライバーは、ドライバーがマスクをサポートするかどうかに関係なく、D3DMULTISAMPLE\_TYPE 列挙型の要素を使用して、複数サンプリングされたサーフェイスのサンプルの数を設定できます。マルチ. ただし、DirectX ランタイムのバージョン9.0 では、ドライバーがマスクとしてビットをサポートしていない限り、DirectX 9.0 以降のドライバーで D3DMULTISAMPLE\_TYPE ビットを DDSCAPS3\_マルチサンプリング\_マスクマスクで設定することはできません。 D3DMULTISAMPLE\_型の詳細については、DirectX SDK のドキュメントを参照してください。

D3DGDI2\_TYPE\_GETFORMATCOUNT クエリでは、DirectX 9.0 ドライバーに、 [**DD\_GETFORMATCOUNTDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_dd_getformatcountdata)構造体の**dwreserved**メンバーのランタイムバージョンが通知されます。 **Dwreserved**メンバーは、DirectX 9.0 の場合は\_ランタイム\_バージョンに設定されます。

D3DGDI2\_TYPE\_GETFORMAT query では、 [**DD\_GETFORMATDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_dd_getformatdata)構造体の**format**メンバーに指定されている ddピクセル形式構造体の**dwSize**メンバーのランタイムバージョンについて、DirectX 9.0 ドライバーに通知されます。 また、 **dwSize**メンバーは、RUNTIME\_バージョン\_にも設定されます。

 

 





