---
title: ACPI キーボードショートカットのロジック
description: ACPI キーボードショートカットのロジック
ms.assetid: cd62380b-1393-403e-b0e6-c52f60c06936
keywords:
- ACPI ホットキー WDK ディスプレイ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 62d06b6ede3abdcbf504afe5f0f9238da5b8b540
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839081"
---
# <a name="acpi-keyboard-shortcut-logic"></a>ACPI キーボードショートカットのロジック


Windows 7 以降では、Ihv は ACPI ベースの OEM 固有のキーボードショートカットを実装しています。 オペレーティングシステムでは、これらのキーボードショートカットは認識されません。 Windows 7 では、Oem は CCD データベースを使用してキーボードショートカットを保存および適用し、オペレーティングシステムとすべての OEM アプリケーションが互いを認識できるようにする必要があります。

Windows 7 で実行されるドライバーの場合、次の関数の呼び出しの動作が変更されています。

<span id="DxgkDdiNotifyAcpiEvent_and_DxgkDdiRecommendFunctionalVidPn"></span><span id="dxgkddinotifyacpievent_and_dxgkddirecommendfunctionalvidpn"></span><span id="DXGKDDINOTIFYACPIEVENT_AND_DXGKDDIRECOMMENDFUNCTIONALVIDPN"></span>[*DxgkDdiNotifyAcpiEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_notify_acpi_event)と[ *DxgkDdiRecommendFunctionalVidPn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_recommendfunctionalvidpn)  
-   ディスプレイミニポートドライバーが DXGK\_\_ACPI を使用して[*DxgkDdiNotifyAcpiEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_notify_acpi_event)関数への呼び出しを受け取った場合、 *AcpiFlags*パラメーターに設定されている\_モードフラグを表示\_には、dmm はを呼び出します[ *。* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_recommendfunctionalvidpn)新しい vidpn を取得し、現在のクライアント vidpn と比較する DxgkDdiRecommendFunctionalVidPn 関数。 2つの VidPNs のトポロジが同じである場合、DMM は新しい VidPN を変更しません。 それ以外の場合、DMM は、トポロジだけを残して、VidPN からモード情報を削除し、CCD データベースが特定のトポロジのモードを判別できるようにします。 次に、DMM は、新しい VidPN に基づいて表示構成を設定します。

<span id="D3DKMTInvalidateActiveVidPn"></span><span id="d3dkmtinvalidateactivevidpn"></span><span id="D3DKMTINVALIDATEACTIVEVIDPN"></span>[**D3DKMTInvalidateActiveVidPn**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtinvalidateactivevidpn)  
-   この機能は、Windows Vista 以降でサポートされています。バージョン &lt; DXGKDDI\_INTERFACE\_VERSION\_WIN7 を使用してミニポートドライバーを表示します。 関数の動作は、Windows Vista での動作と同じです。

-   この関数は、バージョン &gt;= DXGKDDI\_INTERFACE\_VERSION\_WIN7 でのミニポートドライバーの表示については、Windows 7 以降ではサポートされていません。 呼び出された場合は、状態コードの状態\_サポートされていません\_が返されます。

 

 





