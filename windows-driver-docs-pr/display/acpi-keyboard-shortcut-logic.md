---
title: ACPI キーボード ショートカット ロジック
description: ACPI キーボード ショートカット ロジック
ms.assetid: cd62380b-1393-403e-b0e6-c52f60c06936
keywords:
- WDK の ACPI ホット キーを表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4421d388277b2d303ac0b68365632eedc788ffd5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354752"
---
# <a name="acpi-keyboard-shortcut-logic"></a>ACPI キーボード ショートカット ロジック


Windows 7 以降、Ihv は、ACPI ベースの OEM 固有のキーボード ショートカットを実装します。 オペレーティング システムは、次のキーボード ショートカットの認識が。 Windows 7、Oem は CCD データベースを使用して格納し、オペレーティング システムと OEM アプリケーションが互いを認識されるようにキーボード ショートカットを適用する必要があります。

次の関数の呼び出しの動作には、Windows 7 で実行されているドライバーが変更されました。

<span id="DxgkDdiNotifyAcpiEvent_and_DxgkDdiRecommendFunctionalVidPn"></span><span id="dxgkddinotifyacpievent_and_dxgkddirecommendfunctionalvidpn"></span><span id="DXGKDDINOTIFYACPIEVENT_AND_DXGKDDIRECOMMENDFUNCTIONALVIDPN"></span>[*DxgkDdiNotifyAcpiEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_notify_acpi_event)と[ *DxgkDdiRecommendFunctionalVidPn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_recommendfunctionalvidpn)  
-   ディスプレイのミニポート ドライバーへの呼び出しを受信した場合、 [ *DxgkDdiNotifyAcpiEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_notify_acpi_event) 、DXGK で関数を\_ACPI\_変更\_表示\_モード フラグを設定、 *AcpiFlags*パラメーター、DMM 呼び出し、 [ *DxgkDdiRecommendFunctionalVidPn* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_recommendfunctionalvidpn)新しい VidPN を取得して、比較対象とする関数現在のクライアント VidPN します。 2 つの VidPNs のトポロジでは、同一の DMM 新しい VidPN は変更されません。 それ以外の場合、DMM は、トポロジを残して、VidPN からモードの情報を削除し、CCD データベースを特定のトポロジのモードを決定します。 DMM 新しい VidPN に基づいて表示の構成を設定します。

<span id="D3DKMTInvalidateActiveVidPn"></span><span id="d3dkmtinvalidateactivevidpn"></span><span id="D3DKMTINVALIDATEACTIVEVIDPN"></span>[**D3DKMTInvalidateActiveVidPn**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/nf-d3dkmthk-d3dkmtinvalidateactivevidpn)  
-   この関数は、Windows Vista でサポートされている以降のバージョンでの表示のミニポート ドライバー &lt; DXGKDDI\_インターフェイス\_バージョン\_WIN7 します。 関数の動作は、Windows Vista での動作と同じです。

-   Windows 7 とバージョンの表示のミニポート ドライバーの後で、この関数はサポートされていません&gt;= DXGKDDI\_インターフェイス\_バージョン\_WIN7 します。 呼び出されると、ステータス コード状態\_いない\_サポートされているが返されます。

 

 





