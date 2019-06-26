---
title: DirectX VA 2.0 拡張モードの機能の提供
description: DirectX VA 2.0 拡張モードの機能の提供
ms.assetid: 86283ac8-a56c-4da9-a3ef-6f4d694130a7
keywords:
- DirectX ビデオ アクセラレータ WDK の表示、拡張のサポート
- ビデオ アクセラレータ WDK DirectX、拡張のサポート
- VA WDK DirectX、拡張のサポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9d122f7e31ef3f9104638deda2d8b8048bf8cee
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383901"
---
# <a name="providing-capabilities-for-directx-va-20-extension-modes"></a>DirectX VA 2.0 拡張モードの機能の提供


ときにその[ **GetCaps** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps)関数が呼び出されると、ユーザー モードのディスプレイ ドライバーが要求の種類に基づいて、DirectX VA 2.0 拡張モードに対して次の機能を提供します (、で指定される**型**のメンバー、 [ **D3DDDIARG\_GETCAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)構造体、 *pData*パラメーターが指す)。

<span id="D3DDDICAPS_GETEXTENSIONGUIDCOUNT_and_D3DDDICAPS_GETEXTENSIONGUIDS_request_types"></span><span id="d3dddicaps_getextensionguidcount_and_d3dddicaps_getextensionguids_request_types"></span><span id="D3DDDICAPS_GETEXTENSIONGUIDCOUNT_AND_D3DDDICAPS_GETEXTENSIONGUIDS_REQUEST_TYPES"></span>D3DDDICAPS\_GETEXTENSIONGUIDCOUNT と D3DDDICAPS\_GETEXTENSIONGUIDS 要求の種類  
ユーザー モードは、数と拡張機能のモードをサポートしている Guid のリストに、ドライバーを返します。 を表示します。 ランタイムは、まずサポートされている Guid の後にサポートされている Guid の一覧については、要求の数を要求します。

<span id="D3DDDICAPS_GETEXTENSIONCAPS_request_type"></span><span id="d3dddicaps_getextensioncaps_request_type"></span><span id="D3DDDICAPS_GETEXTENSIONCAPS_REQUEST_TYPE"></span>D3DDDICAPS\_GETEXTENSIONCAPS 要求の種類  
ユーザー モードのディスプレイ ドライバーをサポートする各拡張機能モードでは、独自の機能を持つことができます。 ユーザー モードのディスプレイ ドライバーがこれらの機能を返すときに、D3DDDICAPS\_GETEXTENSIONCAPS 要求の種類が渡されます。 Direct3D のランタイムを指定します、 [ **DXVADDI\_QUERYEXTENSIONCAPSINPUT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_dxvaddi_queryextensioncapsinput)変数の機能を取得する GUID の拡張機能の構造を**pInfo**のメンバー [ **D3DDDIARG\_GETCAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)を指します。 ユーザー モードのディスプレイ ドライバーが機能をプライベートの拡張機能 GUID 構造体を返します、 **pData** D3DDDIARG のメンバー\_GETCAPS を指します。

 

 





