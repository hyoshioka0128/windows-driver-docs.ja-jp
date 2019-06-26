---
title: VidPN ハードウェア機能のクエリ
description: VidPN ハードウェア機能のクエリ
ms.assetid: fb7939bb-ff7e-4ba8-b801-ac10010c44b7
keywords:
- VidPN WDK の表示、ハードウェアの機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88bb6f4c110daa46412ae973c8ca82ebdae27849
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385043"
---
# <a name="querying-vidpn-hardware-capabilities"></a>VidPN ハードウェア機能のクエリ


Windows 7 以降、ミニポート ドライバーが指定した機能 VidPN のすべてのハードウェア機能を報告する必要があるされます。 ドライバーには、次のコールバック関数とその関連付けられている構造体をサポートする必要があります。

-   [**DxgkDdiQueryVidPnHWCapability** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_queryvidpnhwcapability)関数

-   [**DXGKARG\_QUERYVIDPNHWCAPABILITY** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_queryvidpnhwcapability)構造体

-   [**D3DKMDT\_VIDPN\_HW\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_hw_capability)構造体

ドライバーでは、ハードウェアの機能をレポート、するときに考慮する回転の一部として行われる暗黙的なプロシージャを複製または拡大縮小の変換: 回転またはスケーリングするには、その前に、ソースを複製する必要がまずします。

D3DKMDT のメンバーのいずれか\_VIDPN\_HW\_機能 VidPN の指定されたパスに意味がない、メンバーが 0 以外の値に設定されている場合、表示モードのマネージャー (DMM) はエラーを報告されませんが。 DMM、ユーザー モードのクライアントに報告する前にこのようなすべての値がクリアされます。 ただし、ドライバーがの値を設定する必要、**占有**D3DKMDT のメンバー\_VIDPN\_HW\_を 0 に機能します。

### <a name="span-idexamplescenariospanspan-idexamplescenariospanexample-scenario"></a><span id="example_scenario"></span><span id="EXAMPLE_SCENARIO"></span>**シナリオ例**

ディスプレイのミニポート ドライバーがハードウェアの機能を報告する方法を表示するには、P1、P2、P3 のハードウェア構成の次の例のセットを検討してください。

-   **P1:** 画面はソース S1 から複製された、90 度回転し、ターゲットに合わせて拡大縮小します。

-   **P2:** 画面は、適用される変換なしでソースの S1 から複製されました。

-   **P3:** S2 のソースに適用される変換はありません。

ときに[ **DxgkDdiQueryVidPnHWCapability** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_queryvidpnhwcapability)が呼び出されると、ドライバーは回転、拡大縮小、複製のメンバーの値を返す必要があります[ **D3DKMDT\_VIDPN\_HW\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_hw_capability)次の表に従って。

返される値のメンバーの D3DKMDT\_VIDPN\_HW\_スケーリング、および変換を複製機能のハードウェア機能 VidPN パス DriverRotation DriverScaling DriverCloning のハードウェアはすべての回転を実行します。

P₁

0

0

0

P₂

0

0

0

P₃

0

0

0

ハードウェアが複製を除くすべての変換を実行できます。

P₁

0

0

0

P₂

0

0

1

P₃

0

0

0

ハードウェアには、クローン作成とスケーリングの変換がない回転を実行できます。 ドライバーは、中間の回転 blit を使用して回転を実行します。

P₁

1

0

0

P₂

0

0

0

P₃

0

0

0

ハードウェアは、複製、スケーリング、または回転の変換を実行できません。 これらの操作は、ドライバーによって実行されます。

P₁

1

1

0

P₂

0

0

1

P₃

0

0

0

 

 

 





