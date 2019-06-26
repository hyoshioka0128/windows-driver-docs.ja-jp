---
title: 完全に型指定されたバック バッファー キャスト
description: 完全に型指定されたバック バッファー キャスト
ms.assetid: d34f95a4-e380-4bfb-9909-0938f63174be
keywords:
- キャスト バック バッファーを完全に型指定された Direct3D バージョン 10.1 WDK Windows 7 表示
- キャスト完全に型指定された戻りバッファーの WDK Windows 7 の表示
- バック バッファーの WDK Windows 7 の表示
- バッファー WDK Windows 7 の表示、型指定された完全バックアップします。
- バック バッファーを完全に型指定された Windows 7 の WDK の表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58b8e7cbc740fdd039ec68e8c4c22b2a0f1ccc31
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372968"
---
# <a name="fully-typed-back-buffers-casting"></a>完全に型指定されたバック バッファー キャスト


このセクションでは、Windows 7 およびそれ以降のオペレーティング システムにのみ適用されます。

ドライバーの呼び出しによって作成されるリソースを検討してください[ **CreateResource(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createresource)関数と、**形式**のメンバー、 [ **。D3D10DDIARG\_CREATERESOURCE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createresource)ファミリ DXGI 形式を設定\_形式\_R8G8B8A8\_TYPELESS、DXGI\_形式\_B8G8R8A8\_TYPELESS または DXGI\_形式\_R10G10B10A2\_TYPELESS と、D3D10\_DDI\_バインド\_で設定値が存在する、 **BindFlags**のメンバー **D3D10DDIARG\_CREATERESOURCE**します。 Direct3D のバージョン 10.1 ランタイムは、適切なファミリの完全に型指定されたメンバーのいずれかを使用してこれらのリソースで、(レンダリング ターゲットまたはシェーダー リソース) ビューを作成後できます (たとえば、DXGI\_形式\_B8G8R8A8\_UNORM\_、DXGI の SRGB\_形式\_B8G8R8A8\_型宣言不要なファミリ) と完全に型指定された元のリソースが作成された場合でも、します。 場合 D3D10\_DDI\_バインド\_リソースには、現在は設定されていません、この再キャストは許可されていません、Direct3D のバージョン 10 では、すべての完全に型指定されたリソースの場合と同様です。

Direct3D のバージョン 10.1 にこの変更により、アプリケーション、DXGI を再表示を\_形式\_R8G8B8A8\_UNORM バック バッファーとして DXGI\_形式\_R8G8B8A8\_UNORM\_SRGB、またはその逆も可能です。 また、この変更により、アプリケーション、DXGI にキャストする\_形式\_B8G8R8A8\_UNORM\_DXGI のバック バッファーを SRGB\_形式\_B8G8R8A8\_UNORM DXGI を再表示します。\_形式\_R10G10B10\_XR\_バイアス\_A2\_DXGI として UNORM\_形式\_R10G10B10A2\_ \*のレンダリングします。

 

 





