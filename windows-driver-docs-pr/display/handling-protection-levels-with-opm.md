---
title: OPM を使用した保護レベルの処理
description: OPM を使用した保護レベルの処理
ms.assetid: 2d3e5d07-8d6f-44fb-985a-96990538ed29
keywords:
- 保護レベル WDK 表示、種類
- 保護レベル WDK 表示、ACP
- 保護レベル WDK 表示、アナログコピー保護
- 保護レベル WDK display、CGMS
- 保護レベル WDK 表示、コンテンツ生成管理システムのアナログ
- 保護レベル WDK 表示、高帯域幅デジタル Content Protection
- 保護レベル WDK ディスプレイ、HDCP
- 保護レベル WDK display、DisplayPort Content Protection
- 保護レベル WDK ディスプレイ、モニター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 888c408ce51ded2a2d88ffe6018f63e34661e793
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838908"
---
# <a name="handling-protection-levels-with-opm"></a>OPM を使用した保護レベルの処理


各出力保護タイプ (たとえば、アナログコピー保護 (ACP)、[コンテンツ生成管理システムアナログ (CGMS)](cgms-a-standards.md)、広帯域デジタル CONTENT PROTECTION (HDCP)、DisplayPort Content Protection ()) には保護レベルがあります。関連付けられています。 ACP の詳細については、 [Rovi (旧称 Macrovision)](https://go.microsoft.com/fwlink/p/?linkid=71273)の web サイトを参照してください。 HDCP の詳細については、「 [Hdcp 仕様のリビジョン 1.1](https://go.microsoft.com/fwlink/p/?linkid=38728)」を参照してください。 DisplayPort の詳細については、 [DisplayPort](https://go.microsoft.com/fwlink/p/?linkid=71382)の Web 記事を参照してください。

グラフィックスアダプターは、出力保護の種類をサポートするためには必要ありません。 ただし、グラフィックスアダプターは、各グラフィックスアダプターの出力に対してサポートされている保護の種類と、各出力に対して現在設定されている保護レベルを正確に報告する必要があります。

ACP と CGMS-A アナログテレビ信号を保護します。 現時点では、OPM は、複合出力、S ビデオ出力、またはコンポーネント出力からの信号を保護するために、ACP と CGMS を使用できます。 さまざまな ACP および CGMS 保護レベルの詳細については、「 [**dxgkmdt\_OPM\_acp\_protection\_LEVEL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_acp_protection_level) 」および「 [**DXGKMDT\_OPM\_CGMSA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_cgmsa)列挙型」を参照してください。

HDCP は、デジタルビデオ信号を保護します。 現時点では、OPM は HDCP を使用して、デジタルビデオインターフェイス (DVI) と高精細マルチメディアインターフェイス (HDMI) コネクタの出力からデータを保護できます。 HDCP 保護レベルの詳細については、「 [**Dxgkmdt\_OPM\_hdcp\_protection\_LEVEL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_hdcp_protection_level)列挙型」を参照してください。

DisplayPort 出力コネクタからのデジタルビデオ信号を保護します。

以下のセクションでは、特定の物理出力コネクタに対して複数の保護された出力が作成された場合の保護レベルの優先順位と、物理出力コネクタの保護レベルを決定するためのアルゴリズムについて説明します。

[保護レベルに優先順位を割り当てる](assigning-precedence-to-protection-levels.md)

[物理出力の保護レベルの決定](determining-the-protection-level-for-a-physical-output.md)

 

 





