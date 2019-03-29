---
title: OPM での保護レベルの処理
description: OPM での保護レベルの処理
ms.assetid: 2d3e5d07-8d6f-44fb-985a-96990538ed29
keywords:
- WDK の保護レベルの種類を表示します。
- 保護レベルの WDK 表示、ACP
- 保護レベルを WDK の表示、コピー防止のアナログ
- 保護レベル、WDK 表示 CGMS A
- 保護レベルのコンテンツ生成管理システムのアナログ、WDK の表示
- 保護レベルの WDK ディスプレイ、高帯域幅デジタル コンテンツ保護
- 保護レベルの WDK 表示、HDCP
- 保護レベルの WDK 表示、ディスプレイ ポート等コンテンツ保護
- 保護レベルの WDK 表示、DPCP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f101195a3dfa4eb8549d9e704b49fd1c98cea70c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577743"
---
# <a name="handling-protection-levels-with-opm"></a>OPM での保護レベルの処理


各出力保護の種類 (たとえば、アナログ コピー防止 (ACP)、[コンテンツ生成管理システム アナログ (CGMS A)](cgms-a-standards.md)、高帯域幅デジタル コンテンツの保護 (HDCP)、およびディスプレイ ポート等コンテンツ保護 (DPCP)) が保護レベルが関連付けられています。 ACP の詳細については、次を参照してください。、 [Rovi (旧称 Macrovision)](https://go.microsoft.com/fwlink/p/?linkid=71273) web サイト。 HDCP の詳細については、次を参照してください。、 [HDCP 仕様のリビジョン 1.1](https://go.microsoft.com/fwlink/p/?linkid=38728)します。 ディスプレイ ポート等の詳細については、次を参照してください。、[ディスプレイ ポート等](https://go.microsoft.com/fwlink/p/?linkid=71382)Web 記事。

グラフィックス アダプターは、任意の出力保護の種類をサポートする必要はありません。 ただし、グラフィックス アダプターをする必要があります、グラフィックス アダプターの出力は、現在設定されている各のサポートされる保護の種類正確にレポートの各出力の保護レベル。

ACP および CGMS A 保護アナログ テレビ信号。 OPM が ACP を使用して現在のところ、および CGMS-A 複合出力、s-ビデオ出力、またはコンポーネントの出力からの信号を保護します。 さまざまな ACP および CGMS A 保護については、レベルを参照してください、 [ **DXGKMDT\_OPM\_ACP\_保護\_レベル**](https://msdn.microsoft.com/library/windows/hardware/ff560834)と[**DXGKMDT\_OPM\_CGMSA** ](https://msdn.microsoft.com/library/windows/hardware/ff560846)列挙体。

HDCP がデジタル ビデオ信号を保護します。 現時点では、OPM で HDCP を使用して、デジタル ビデオ インターフェイス (DVI) および高品位のマルチ メディア インターフェイス (HDMI) コネクタの出力からデータを保護することができます。 HDCP 保護のレベルについては、次を参照してください。、 [ **DXGKMDT\_OPM\_HDCP\_保護\_レベル**](https://msdn.microsoft.com/library/windows/hardware/ff560878)列挙体。

DPCP は、ディスプレイ ポート等出力コネクタからデジタル ビデオ信号を保護します。

次のセクションでは、特定の物理出力コネクタと物理出力コネクタの保護レベルを決定するためのアルゴリズムの 1 つ以上の保護されている出力が作成された場合、保護レベルに配置されている優先順位について説明します。

[保護レベルに優先順位を割り当てる](assigning-precedence-to-protection-levels.md)

[物理的な出力の保護レベルを決定します。](determining-the-protection-level-for-a-physical-output.md)

 

 





