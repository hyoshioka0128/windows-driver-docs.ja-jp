---
title: AV/C ストリーミングの概要
description: AV/C ストリーミングの概要
ms.assetid: c500fad7-26b7-4507-953e-258dd9c91253
keywords:
- AV/C WDK、ストリームフィルタードライバー
- ストリームフィルタードライバー WDK AV/C
- Avcstrm.sys ストリーミングフィルタードライバー WDK
- Avcstrm.sys ストリーミングフィルタードライバー WDK、Avcstrm.sys ストリーミングフィルタードライバーについて
- フィルタードライバー WDK AV/C streaming
ms.date: 06/15/2020
ms.localizationpriority: medium
ms.openlocfilehash: dd615dc57f70d50a06368952dfcd304558377955
ms.sourcegitcommit: 77c63789350cfc1dc740baaafdef64803d86217f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/16/2020
ms.locfileid: "84793734"
---
# <a name="avc-streaming-overview"></a>AV/C ストリーミングの概要

このセクションでは、AV/c ストリーミングフィルタードライバーの*Avcstrm.sys*について説明します。これは、データが sddv または MPEG2TS 形式の場合、Av/c サブユニットからのメディアデータのストリーミングを支援するために Microsoft が提供します。 これらの形式は、デジタルデータをメディア信号に格納するための最も一般的な2つの方法です。

*Avcstrm.sys*は、 *Avc.sys*のすぐ上に配置される下位サブレベルのフィルタードライバーであり、ドライバースタックおよびサブユニットドライバーの下に*61883.sys*ます。 AV/C ストリームフィルタードライバーは、AV/C プロトコルドライバーの追加サポートを提供します。 これは、ベンダーがこのサポートを使用する場合は省略可能です。

テープサブユニット仕様 ( [1394 の取引アソシエーション](https://1394ta.org/library-2)web サイトにあります) は、メディア信号に関係なく、再生、一時停止、記録、停止などのさまざまなトランスポート状態制御をサポートしています。 ただし、同じサブユニットの種類のデータ形式は同じまたは異なる場合があります。 たとえば、DV デバイスと DVHS デバイスの両方に tape サブユニットが含まれています。 ただし、DV では通常、IEC 61883-2 仕様に基づく SDDV データ形式が使用されますが、DVHS では61883-4 仕様に基づく MPEG2TS データ形式が使用されます。 このため、tape サブユニットのフィルタードライバーは SDDV と MPEG2TS の両方のデータ形式をサポートする必要がありますが、テープサブユニットには同じデバイス制御を使用してください。 これは、すべてのサブユニットドライバーが、形式を認識するストリーミング機能を提供するために、同じ機能を複製する必要があることを意味します。

61883および AV/C サブユニットドライバースタックで AV/C サブユニットドライバーを制御するには、61883プロトコルドライバーによって提供されるデバイスドライバーインターフェイス (DDIs) を使用して、データストリームを受信または転送するドライバー関数が必要です。 これらのドライバー関数は、次の操作を実行します。

- アイソクロナスリソースを割り当て、アイソクロナス接続を確立する

- キューデータバッファー

- データバッファーの受信または転送の完了と終了

- スレッド間でストリームの状態を同期する

AV/C ストリームフィルタードライバーは、 *61883.sys*プロトコルドライバーに依存しています。 *Avcstrm.sys*は、 *61883.sys*によって提供される DDIs を使用して、アイソクロナス接続とアイソクロナスデータストリーミングを実行し、 *Avc.sys*を使用して外部デバイスコントロールの AV/C コマンドを発行します。

Av/c ストリーミングフィルタドライバが構築される AV/C プロトコルの詳細については、「 [av/c の概要](av-c-overview.md)」を参照してください。 61883プロトコルの詳細については、「 [IEC-61883 クライアントドライバー](https://docs.microsoft.com/windows-hardware/drivers/ieee/iec-61883-client-drivers)」を参照してください。

詳細とリソースについては、次のリンクを参照してください。

[Windows Driver Model](https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-driver-model)

[1394取引関係の仕様](https://1394ta.org/library-2)

[国際電気技術標準機関 (International Electrotechnical Commission)](https://www.iec.ch/)
