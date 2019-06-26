---
title: Direct3D バージョン 9 ドライバーの DDI 変更
description: Direct3D バージョン 9 ドライバーの DDI 変更
ms.assetid: b702c02d-3be6-46e8-9e53-5d33e5e3fc70
keywords:
- Direct3D のバージョン 9 ドライバーの Direct3D バージョン 10.1 WDK Windows 7 の表示、DDI の変更します。
- Direct3D のバージョン 9 ドライバー WDK Windows 7 を表示します。
- Direct3D のバージョン 9 ドライバー WDK Windows 7 の表示、DDI の変更します。
- XR_BIAS WDK Windows 7 の表示、Direct3D のバージョン 9 DDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ad4249404fbdb6131b87a3f4640280695094014
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365099"
---
# <a name="ddi-changes-for-direct3d-version-9-drivers"></a>Direct3D バージョン 9 ドライバーの DDI 変更


このセクションでは、Windows 7 およびそれ以降のオペレーティング システムにのみ適用されます。

XR\_バイアスは、Windows 7 にのみ、Direct3D のバージョン 9 をサポートするユーザー モードのディスプレイ ドライバーを使用できるように書式設定機能を拡張のみ新しい DDI します。

このようなユーザー モードのディスプレイ ドライバーは、D3DDDIFMT をサポートしていることを示すことができます\_A2B10G10R10\_XR\_バイアス形式の値から、 [ **D3DDDIFORMAT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ne-d3dukmdt-_d3dddiformat)列挙体です。 ドライバーでは、このようなサポートを示すの配列内のエントリを作成して設定された[ **FORMATOP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_formatop)内の構造体、 **pData**のメンバー、 [ **D3DDDIARG\_GETCAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)構造体への呼び出しからドライバーを返す、 [ **GetCaps** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps) D3DDDICAPS で関数を\_GETFORMATDATA 値の設定、**型**D3DDDIARG のメンバー\_GETCAPS します。 このエントリを示すため、**操作**のメンバー **FORMATOP**、すべてのランタイムは、D3DDDIFMT とサーフェスで実行できる一般的な操作\_A2B10G10R10\_XR\_バイアス形式。 たとえば、ドライバーは、FORMATOP を設定する必要があります\_\*\_レンダリング ターゲットのビットで**操作**します。 ドライバーは、FORMATOP を設定する必要がありますも\_DISPLAYMODE と FORMATOP\_3DACCELERATION ビットで**操作**します。

ドライバーが返された場合、 [ **FORMATOP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_formatop)エントリ、D3DDDIFMT\_A2B10G10R10\_XR\_バイアス形式、その後、ドライバーはそのへの呼び出しを受信します。[**CreateResource** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource) 、D3DDDIFMT のリソースを作成する関数\_A2B10G10R10\_XR\_バイアス形式の設定、**形式**のメンバー、 [ **D3DDDIARG\_CREATERESOURCE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)構造体。

ドライバーのみ、D3DDDIFMT のリソースを作成する要求を受信する\_A2B10G10R10\_XR\_フリッピング チェーンの全画面表示のバイアス形式。 Windows デスクトップ マネージャー (DWM) XR のウィンドウのプレゼンテーションを処理する\_シェーダー コードのバイアス。 ドライバーが D3DDDIFMT を扱う必要があります\_A2B10G10R10\_XR\_バイアス形式のリソースとして、D3DDDIFMT\_A2B10G10R10 がスキャンを除くすべての操作で書式設定、ドライバーが D3DDDIFMT を扱うことができます、\_A2B10G10R10\_XR\_バイアス形式のリソースとして、D3DDDIFMT\_ブレンド、フィルター、および形式変換の操作の A2B10G10R10 形式。 唯一の違いはどのように XR\_バイアス スキャン アウトに影響を与えます。スキャン アウトの詳細については、次を参照してください。 [BGRA スキャン アウト サポート](bgra-scan-out-support.md)します。

 

 





