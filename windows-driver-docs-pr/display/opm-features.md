---
title: OPM 機能
description: OPM 機能
ms.assetid: a2fc9d0c-d85c-484e-8cf2-09b2a84801f8
keywords:
- OPM WDK の表示の機能
- OPM WDK の表示、COPP と OPM の比較
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f374d97e66c3699b1b5b18f57c7e0bb72fdb02d7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551810"
---
# <a name="opm-features"></a>OPM 機能

OPM は認定出力保護プロトコルの (COPP) をすべてサポート機能。 一部の新しい OPM 機能と OPM の一部の機能と COPP 機能との比較を次に示します。

-   OPM では、アプリケーションについては、ビデオ出力 COPP でアプリケーションについては、グラフィックス ドライバーからの要求に署名することが必要ありませんからの要求に署名することが必要です。

    > [!NOTE]
    > COPP グラフィック ドライバーは、OPM ビデオの出力と同じです。

    COPP アプリケーションでは、グラフィックス ドライバーから情報を要求、それによって、 [ **DXVA\_COPPStatusInput** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_coppstatusinput)ドライバーに渡される構造体。

-   OPM には、高帯域幅デジタル コンテンツの保護 (HDCP) リピータがサポートされています。 HDCP リピータの詳細については、、 [HDCP 仕様のリビジョン 1.1](https://go.microsoft.com/fwlink/p/?linkid=38728)を参照してください。

-   アプリケーションは、OPM で HDCP をより簡単にサポートできます。 アプリケーションは、HDCP システム Renewability メッセージ (SRMs) を解析し、モニターが取り消されたかどうかを決定する必要はありません。 HDCP SRMs の詳細については、、 [HDCP 仕様のリビジョン 1.1](https://go.microsoft.com/fwlink/p/?linkid=38728)を参照してください。

-   OPM が X.509 証明書を使用し、COPP が独自の XML の証明書を使用します。 COPP 証明書の形式は、XML 署名の構文と処理の仕様での署名の形式に基づきます。 X.509 証明書については、、 [X.509 証明書プロファイル](https://go.microsoft.com/fwlink/p/?linkid=70416)を参照してください。

-   COPP アプリケーションの取得、COPP **IAMCertifiedOutputProtection**インターフェイス バージョン 7 または 9 のビデオの混在レンダラーを作成して ([*VMR*](https://docs.microsoft.com/windows/desktop/DirectShow/using-the-video-mixing-renderer)) IIDを渡します\_VMR フィルターの実装に IAMCertifiedOutputProtection **iunknown::queryinterface**します。 アプリケーションが OPM、 **IOPMVideoOutput** 、HMONITOR を渡すことによってインターフェイスまたは**IDirect3DDevice9**オブジェクトを**OPMGetVideoOutputsFromHMONITOR**または**OPMGetVideoOutputsFromIDirect3DDevice9Object**それぞれに機能します。 これらの関数とインターフェイスの詳細については、Microsoft Windows SDK のドキュメントを参照してください。

-   OPM は、COPP 複製モードでは、1 つの特定のケースのみがサポートされますが、すべてのケースで複製モードをサポートします。

-   OPM の再配布制御フラグが COPP の再配布制御フラグとは若干異なるセマンティクス (COPP\_CGMSA\_RedistributionControlRequired)。