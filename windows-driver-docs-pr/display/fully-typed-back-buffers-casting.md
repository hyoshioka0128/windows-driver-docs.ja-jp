---
title: 完全に型指定されたバックバッファーのキャスト
description: 完全に型指定されたバックバッファーのキャスト
ms.assetid: d34f95a4-e380-4bfb-9909-0938f63174be
keywords:
- Direct3D バージョン 10.1 WDK Windows 7 display、完全に型指定されたバックバッファーのキャスト
- 完全に型指定されたバックバッファーをキャストする WDK Windows 7 ディスプレイ
- バックバッファー WDK Windows 7 ディスプレイ
- バックバッファー WDK Windows 7 display、完全に型指定
- 完全に型指定されたバックバッファー WDK Windows 7 ディスプレイ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef211bc2376b7952b8c36d61c600731f06d9d9fe
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839687"
---
# <a name="fully-typed-back-buffers-casting"></a>完全に型指定されたバックバッファーのキャスト


このセクションは、Windows 7 以降のオペレーティングシステムにのみ適用されます。

[**D3D10DDIARG\_createresource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createresource)構造体の**format**メンバーを family DXGI\_形式の形式に設定して、ドライバーの[**createresource (D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createresource)関数の呼び出しによって作成されるリソースを検討してください\_R8G8B8A8\_型指定されていない、DXGI\_形式\_B8G8R8A8\_タイプレスまたは DXGI\_形式\_R10G10B10A2\_型指定なし、D3D10\_DDI\_バインド\_**D3D10DDIARG の BindFlags**メンバー **\_createresource**。 その後、Direct3D バージョン10.1 ランタイムは、適切なファミリの完全に型指定されたメンバー (たとえば、DXGI\_形式\_B8G8R8A8\_UNORM) を使用して、これらのリソースに対してビュー (レンダーターゲットまたはシェーダーリソース) を作成でき @no__t_最初のリソースが完全に型指定されたものとして作成されている場合でも、DXGI\_形式\_B8G8R8A8\_タイプなしファミリ) の場合は、3_ SRGB。\_ D3D10\_DDI\_BIND\_PRESENT がリソースに対して設定されていない場合、Direct3D バージョン10のすべての完全に型指定されたリソースの場合と同様に、この再キャストは許可されません。

この Direct3D バージョン10.1 の変更により、アプリケーションでは、DXGI\_形式\_R8G8B8A8\_UNORM バックバッファーを DXGI\_形式で再表示できるようになります。これは、R8G8B8A8\_UNORM\_SRGB およびその逆です。\_ また、この変更により、アプリケーションは、dxgi\_形式\_B8G8R8A8\_UNORM\_SRGB バックバッファーを使用して、B8G8R8A8\_UNORM\_、dxgi\_形式\_R10G10B10 を再表示することもでき\_9_ XR\_バイアスは、レンダリングのために\_A2\_を DXGI\_形式\_R10G10B10A2\_\* として使用します。\_

 

 





