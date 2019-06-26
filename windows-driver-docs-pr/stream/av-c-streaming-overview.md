---
title: AV/C ストリーミングの概要
description: AV/C ストリーミングの概要
ms.assetid: c500fad7-26b7-4507-953e-258dd9c91253
keywords:
- AV/C WDK、Stream フィルター ドライバー
- フィルター ドライバー WDK AV/C を Stream
- Avcstrm.sys ストリーミング フィルター ドライバー WDK
- Avcstrm.sys Avcstrm.sys ストリーミング フィルター ドライバーの詳細については、フィルター ドライバー WDK、ストリーミング
- フィルター ドライバー WDK AV/C のストリーミング
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fbf100cd30e67d04b732019bf2abf4b2d66058bf
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386745"
---
# <a name="avc-streaming-overview"></a>AV/C ストリーミングの概要

このセクションには、AV/C ストリーミング フィルター ドライバーがについて説明します*Avcstrm.sys*、ストリーミングでは、そのデータがいずれかの SDDV か MPEG2TS 形式を AV/C サブユニットからメディア データで支援するためにマイクロソフトが提供しています。 これらの形式は、メディア信号にデジタル データを格納するための 2 つの最も一般的な方法です。

*Avcstrm.sys*の上にすぐに配置する下位レベルのサブユニット フィルター ドライバーは、 *Avc.sys*と*61883.sys*ドライバー スタックでは以下のすべてのサブユニット ドライバー。 AV/C Stream フィルター ドライバーは、AV/C プロトコル ドライバーの追加のサポートを提供します。 このコマンドは、このサポートを使用する仕入先を省略できます。

テープのサブユニット仕様 (にある、 [1394 貿易](https://go.microsoft.com/fwlink/p/?LinkId=518448)web サイト) play など、さまざまなトランスポート状態のサポートのコントロール、一時停止、記録およびそのメディア信号に関係なく、停止します。 ただし、同じのサブユニット型のデータ形式にすることができます、同じまたは異なる。 たとえば、DV と DVHS の両方のデバイスには、テープのサブユニットが含まれています。 ただし、DV では通常 IEC 61883 2 の仕様に基づいている SDDV データ形式を使用して、一方、DVHS 61883 4 仕様に基づいている MPEG2TS データ形式を使用します。 テープのサブユニットのフィルター ドライバーの SDDV と MPEG2TS の両方のデータ形式をサポートがテープのサブユニットを同じデバイスの制御を使用する必要があるため。 これは、ため、すべてのサブユニット ドライバーがストリーミング形式を認識する機能を提供する同じ機能を複製する必要があります。

61883 および AV/C サブユニット ドライバー スタック上の AV/C サブユニット ドライバーを制御するには、61883 プロトコル ドライバーによって提供されるデバイス ドライバー インターフェイス (Ddi) を使用してデータ ストリームを送信または受信をドライバー関数が必要です。 これらのドライバー関数は、次の操作を実行します。

- アイソクロナス リソースを割り当てるし、アイソクロナス接続を作成します。

- キューのデータ バッファー

- アタッチし、受信または送信データ バッファーの完了

- スレッド間でのストリームの状態を同期します。

AV/C Stream フィルター ドライバーに依存、 *61883.sys*プロトコル ドライバー。 *Avcstrm.sys*使用によって提供される Ddi *61883.sys*アイソクロナス接続とアイソクロナス データがストリーミングとそれを実行するために*Avc.sys*外部デバイスの制御 AV/C コマンドを発行するには.

AV/C ストリーミング フィルター ドライバーの構築、AV/C プロトコルの詳細については、次を参照してください。 [AV/C 概要](av-c-overview.md)します。 61883 プロトコルの詳細については、次を参照してください。 [IEC 61883 クライアント ドライバー](https://docs.microsoft.com/windows-hardware/drivers/ieee/iec-61883-client-drivers)します。

詳細情報とリソースは、次のリンクを参照してください。

[Windows Driver Model](https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-driver-model)

[1394 貿易仕様](https://go.microsoft.com/fwlink/p/?linkid=518448)

[International Electrotechnical Commission](https://go.microsoft.com/fwlink/p/?linkid=8732)
