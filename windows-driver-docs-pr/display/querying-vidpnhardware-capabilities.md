---
title: VidPN ハードウェア機能のクエリ
description: VidPN ハードウェア機能のクエリ
ms.assetid: fb7939bb-ff7e-4ba8-b801-ac10010c44b7
keywords:
- VidPN WDK ディスプレイ、ハードウェア機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8c9aafe2bb105868b05234a0491697907348aa2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825958"
---
# <a name="querying-vidpn-hardware-capabilities"></a>VidPN ハードウェア機能のクエリ


Windows 7 以降では、指定された機能的な VidPN のすべてのハードウェア機能をレポートするために、表示ミニポートドライバーが必要です。 ドライバーは、次のコールバック関数とそれに関連付けられている構造体をサポートする必要があります。

-   [**DxgkDdiQueryVidPnHWCapability**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryvidpnhwcapability)関数

-   [**Dxgkarg\_QUERYVIDPNHWCAPABILITY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_queryvidpnhwcapability)構造体

-   [**D3DKMDT\_VIDPN\_HW\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_hw_capability)の構造

ドライバーがハードウェアの機能を報告する場合、複製は、回転やスケーリングの変換の一部として実行される暗黙の手順として使用することを検討する必要があります。最初にソースを複製してから、回転または拡大縮小する必要があります。

D3DKMDT\_VIDPN\_HW\_機能のいずれかのメンバーが、指定された VidPN パスで意味を持たない場合、メンバーが0以外の値に設定されていると、表示モードマネージャー (DMM) はエラーを報告しません。 DMM は、ユーザーモードクライアントに報告する前に、このようなすべての値をクリアします。 ただし、ドライバーでは、D3DKMDT\_VIDPN\_HW\_機能の**予約**メンバーの値を0に設定する必要があります。

### <a name="span-idexample_scenariospanspan-idexample_scenariospanexample-scenario"></a><span id="example_scenario"></span><span id="EXAMPLE_SCENARIO"></span>**シナリオ例**

ディスプレイミニポートドライバーがハードウェアの機能を報告する方法を示すために、次のようなハードウェア構成の P1、P2、P3 のセットの例を考えてみましょう。

-   **P1:** Surface はソース S1 から複製された後、90°回転し、ターゲットに合わせて拡大縮小されます。

-   **P2:** Surface は、変換が適用されていないソース S1 から複製されます。

-   **P3:** ソース S2 には適用された変換がありません。

[**DxgkDdiQueryVidPnHWCapability**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryvidpnhwcapability)が呼び出されると、ドライバーは、次の表に従って、 [**D3DKMDT\_VIDPN\_HW\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_hw_capability)のメンバーのローテーション、拡大縮小、および複製のための値を返します。

D3DKMDT のメンバーの戻り値\_VIDPN\_HW\_機能のハードウェア機能については、「VidPN パス DriverRotation Driverrotation Driverrotation」ハードウェアでは、すべてのローテーション、スケーリング、複製変換を実行できます。

P ₁

0

0

0

P ₂

0

0

0

P ₃

0

0

0

複製を除くすべての変換を実行できるハードウェア

P ₁

0

0

0

P ₂

0

0

1

P ₃

0

0

0

ハードウェアは複製とスケーリングの変換を実行できますが、ローテーションは実行できません。 ドライバーは、中間ローテーション array.blit を使用して回転を実行します。

P ₁

1

0

0

P ₂

0

0

0

P ₃

0

0

0

ハードウェアは、複製、拡大縮小、または回転変換を実行できません。 これらの操作はドライバーによって実行されます。

P ₁

1

1

0

P ₂

0

0

1

P ₃

0

0

0

 

 

 





