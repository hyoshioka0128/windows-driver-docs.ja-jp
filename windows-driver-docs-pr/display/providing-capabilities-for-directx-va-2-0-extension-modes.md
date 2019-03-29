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
ms.openlocfilehash: dfdbfa68ea84703031c1505a2cd798d12feffce8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577887"
---
# <a name="providing-capabilities-for-directx-va-20-extension-modes"></a>DirectX VA 2.0 拡張モードの機能の提供


ときにその[ **GetCaps** ](https://msdn.microsoft.com/library/windows/hardware/ff566762)関数が呼び出されると、ユーザー モードのディスプレイ ドライバーが要求の種類に基づいて、DirectX VA 2.0 拡張モードに対して次の機能を提供します (、で指定される**型**のメンバー、 [ **D3DDDIARG\_GETCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff543148)構造体、 *pData*パラメーターが指す)。

<span id="D3DDDICAPS_GETEXTENSIONGUIDCOUNT_and_D3DDDICAPS_GETEXTENSIONGUIDS_request_types"></span><span id="d3dddicaps_getextensionguidcount_and_d3dddicaps_getextensionguids_request_types"></span><span id="D3DDDICAPS_GETEXTENSIONGUIDCOUNT_AND_D3DDDICAPS_GETEXTENSIONGUIDS_REQUEST_TYPES"></span>D3DDDICAPS\_GETEXTENSIONGUIDCOUNT と D3DDDICAPS\_GETEXTENSIONGUIDS 要求の種類  
ユーザー モードは、数と拡張機能のモードをサポートしている Guid のリストに、ドライバーを返します。 を表示します。 ランタイムは、まずサポートされている Guid の後にサポートされている Guid の一覧については、要求の数を要求します。

<span id="D3DDDICAPS_GETEXTENSIONCAPS_request_type"></span><span id="d3dddicaps_getextensioncaps_request_type"></span><span id="D3DDDICAPS_GETEXTENSIONCAPS_REQUEST_TYPE"></span>D3DDDICAPS\_GETEXTENSIONCAPS 要求の種類  
ユーザー モードのディスプレイ ドライバーをサポートする各拡張機能モードでは、独自の機能を持つことができます。 ユーザー モードのディスプレイ ドライバーがこれらの機能を返すときに、D3DDDICAPS\_GETEXTENSIONCAPS 要求の種類が渡されます。 Direct3D のランタイムを指定します、 [ **DXVADDI\_QUERYEXTENSIONCAPSINPUT** ](https://msdn.microsoft.com/library/windows/hardware/ff562926)変数の機能を取得する GUID の拡張機能の構造を**pInfo**のメンバー [ **D3DDDIARG\_GETCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff543148)を指します。 ユーザー モードのディスプレイ ドライバーが機能をプライベートの拡張機能 GUID 構造体を返します、 **pData** D3DDDIARG のメンバー\_GETCAPS を指します。

 

 





