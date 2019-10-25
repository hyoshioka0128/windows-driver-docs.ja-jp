---
title: OPM の機能
description: OPM の機能
ms.assetid: a2fc9d0c-d85c-484e-8cf2-09b2a84801f8
keywords:
- OPM WDK の表示、機能
- OPM WDK display、COPP、OPM の比較
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92208d4b15d29032377b4e49b07c74b1205e8335
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840493"
---
# <a name="opm-features"></a>OPM の機能

OPM は、すべての認定出力保護プロトコル (COPP) 機能をサポートしています。 ここでは、いくつかの新しい OPM 機能と、一部の OPM 機能を COPP 機能と比較する方法について説明します。

-   OPM では、アプリケーションがビデオ出力からの情報に対する要求に署名する必要がありますが、COPP では、アプリケーションがグラフィックスドライバーからの情報を要求する必要はありません。

    > [!NOTE]
    > COPP グラフィックスドライバーは、OPM ビデオ出力に相当します。

    COPP アプリケーションは、 [**DXVA\_COPPStatusInput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatusinput)構造体をドライバーに渡すことによって、グラフィックスドライバーから情報を要求します。

-   OPM は、高帯域幅のデジタル Content Protection (HDCP) リピータをサポートしています。 HDCP リピータの詳細については、「 [Hdcp 仕様のリビジョン 1.1](https://go.microsoft.com/fwlink/p/?linkid=38728)」を参照してください。

-   アプリケーションは、OPM の HDCP をより簡単にサポートできます。 アプリケーションは、HDCP システムの Renewability メッセージ (SRMs) を解析し、モニターが取り消されたかどうかを判断するためには必要ありません。 HDCP の詳細については、「 [Hdcp 仕様のリビジョン 1.1](https://go.microsoft.com/fwlink/p/?linkid=38728)」を参照してください。

-   OPM は x.509 証明書を使用し、COPP は独自の XML 証明書を使用します。 COPP 証明書の形式は、XML 署名の構文と処理仕様の署名形式に基づいています。 X.509 証明書の詳細については、 [X.509 証明書プロファイル](https://go.microsoft.com/fwlink/p/?linkid=70416)を参照してください。

-   COPP アプリケーションは、ビデオミキシングレンダラー ([*VMR*](https://docs.microsoft.com/windows/desktop/DirectShow/using-the-video-mixing-renderer)) のバージョン7または9を作成し、IID\_IAMCERTIFIEDOUTPUTPROTECTION を VMR フィルターの実装 **に渡すことによって、copp IAMCertifiedOutputProtection インターフェイスを取得します。IUnknown:: QueryInterface**。 OPM アプリケーションは、HMONITOR または**IDirect3DDevice9**オブジェクトを**Opmgetvideooutputsfromhmonitor**または**OPMGetVideoOutputsFromIDirect3DDevice9Object**関数に渡すことによって、 **IOPMVideoOutput**インターフェイスを取得します。4.3. これらの関数とインターフェイスの詳細については、Microsoft Windows SDK のドキュメントを参照してください。

-   OPM は常に複製モードをサポートしていますが、COPP では複製モードが1つの特定のケースでのみサポートされています。

-   OPM の再配布制御フラグは、COPP の再配布制御フラグ (COPP\_CGMSA\_RedistributionControlRequired) とは若干異なるセマンティクスを持ちます。