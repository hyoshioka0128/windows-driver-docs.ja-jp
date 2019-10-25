---
title: DirectX VA 2.0 拡張モードの機能の提供
description: DirectX VA 2.0 拡張モードの機能の提供
ms.assetid: 86283ac8-a56c-4da9-a3ef-6f4d694130a7
keywords:
- DirectX ビデオアクセラレーション WDK ディスプレイ、拡張サポート
- ビデオアクセラレーション WDK DirectX、拡張サポート
- VA WDK DirectX、拡張サポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4eb4af9bebe2b5fe0a66312e9898c0ef74e87126
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826034"
---
# <a name="providing-capabilities-for-directx-va-20-extension-modes"></a>DirectX VA 2.0 拡張モードの機能の提供


[**Getcaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps)関数が呼び出されると、ユーザーモード表示ドライバーは、要求の種類に基づいて DirectX VA 2.0 拡張モード用の次の機能を提供します ( [**D3DDDIARG\_getcaps の type メンバーで指定されています)。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps) *pData*パラメーターが指す構造体。

<span id="D3DDDICAPS_GETEXTENSIONGUIDCOUNT_and_D3DDDICAPS_GETEXTENSIONGUIDS_request_types"></span><span id="d3dddicaps_getextensionguidcount_and_d3dddicaps_getextensionguids_request_types"></span><span id="D3DDDICAPS_GETEXTENSIONGUIDCOUNT_AND_D3DDDICAPS_GETEXTENSIONGUIDS_REQUEST_TYPES"></span>D3DDDICAPS\_GETEXTENSIONGUIDCOUNT と D3DDDICAPS\_GETEXTENSIONGUID 要求の種類  
ユーザーモード表示ドライバーでは、拡張モードでサポートされている Guid の番号と一覧が返されます。 ランタイムはまず、サポートされている Guid の数を要求し、次にサポートされている Guid の一覧を要求します。

<span id="D3DDDICAPS_GETEXTENSIONCAPS_request_type"></span><span id="d3dddicaps_getextensioncaps_request_type"></span><span id="D3DDDICAPS_GETEXTENSIONCAPS_REQUEST_TYPE"></span>D3DDDICAPS\_GETEXTENSIONCAPS 要求の種類  
ユーザーモード表示ドライバーでサポートされている各拡張モードは、固有の機能を持つことができます。 ユーザーモードの表示ドライバーは、D3DDDICAPS\_GETEXTENSIONCAPS 要求の種類が渡されたときにこれらの機能を返します。 Direct3D ランタイムは、 [**D3DDDIARG\_GETCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps) **が指す**変数での機能を取得するために、拡張機能の GUID の[**DXVADDI\_QUERYEXTENSIONCAPSINPUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvaddi_queryextensioncapsinput)構造体を指定します。 ユーザーモード表示ドライバーは、\_D3DDDIARG の**pData**メンバーが指すプライベート構造体の拡張 GUID の機能を返します。

 

 





