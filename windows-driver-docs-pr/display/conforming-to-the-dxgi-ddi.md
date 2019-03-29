---
title: DXGI DDI への準拠
description: DXGI DDI への準拠
ms.assetid: 1c789f57-003e-4b29-9a81-dbf194670664
keywords:
- Direct3D のバージョン 11 WDK Windows 7 の表示、DXGI DDI 準拠
- Direct3D のバージョン 11 WDK Windows Server 2008 R2 表示、DXGI DDI 準拠
- DirectX グラフィックス インフラストラクチャ DDI 準拠 WDK Windows 7 の表示
- DirectX グラフィックス インフラストラクチャ DDI 準拠 WDK Windows Server 2008 R2 の表示
- DXGI DDI 準拠 WDK Windows 7 の表示
- DXGI DDI 準拠 WDK Windows Server 2008 R2 の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 182fbb7d58a4588850560a912245fa82d7fe799b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581219"
---
# <a name="conforming-to-the-dxgi-ddi"></a>DXGI DDI への準拠


このセクションでは、Windows 7 以降および Windows Server 2008 R2 以降のバージョンの Windows オペレーティング システムにのみ適用されます。

Direct3D のバージョン 11 に準拠している DDI、 [DirectX Graphics Infrastructure (DXGI) DDI の](directx-graphics-infrastructure-ddi.md)リソース インターフェイス、デバイスの列挙、およびプレゼンテーションを定義します。

### <a name="span-idpresentationspanspan-idpresentationspanpresentation"></a><span id="presentation"></span><span id="PRESENTATION"></span>プレゼンテーション

Direct3D のバージョン 11 デバイスは、すべてスキャン アウト可能な形式からプレゼンテーションをサポートする必要があります。、ためには、ユーザー モードのディスプレイ ドライバーが色変換を呼び出す、ディスプレイ ミニポート ドライバー (カーネル モード ドライバー) をフィールドの存在操作する必要があります。すべての他のスキャン アウト形式ともに標準の GDI スキャン アウト形式にスキャン アウト形式のいずれか。 これらのスキャン アウト形式は、DXGI から、次の値によって把握されて\_形式の列挙体。

-   DXGI\_形式\_B5G6R5\_UNORM

-   DXGI\_形式\_B5G5R5A1\_UNORM

-   DXGI\_形式\_B8G8R8A8\_UNORM

-   DXGI\_形式\_B8G8R8X8\_UNORM

Direct3D のバージョン 11 を同梱バック バッファーの制限がある DDI します。 場合 DXGI\_使用状況\_バックバッファー (から、 [DXGI\_使用状況](https://go.microsoft.com/fwlink/p/?linkid=122799)列挙型) が設定された場合、次に、その他の DXGI 箇所だけ許可されています。

-   DXGI\_使用状況\_D3D11 にマップする、SHADERINPUT\_バインド\_シェーダー\_リソース

-   DXGI\_使用状況\_レンダリング\_ターゲット\_D3D11 にマップする出力\_バインド\_レンダリング\_ターゲット

バック バッファーの CPU アクセス フラグが許可されないことに注意してください。

 

 





