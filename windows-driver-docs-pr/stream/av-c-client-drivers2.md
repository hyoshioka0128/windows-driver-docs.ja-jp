---
title: AV/C クライアント ドライバー
description: AV/C クライアント ドライバー
ms.assetid: 70d98c31-2da6-455b-91d8-59bed306b574
keywords:
- AVStream WDK、AV/C
- AV/C WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d5e71d8913ce0fbc98083be2daaa52a2bd3d2784
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386770"
---
# <a name="avc-client-drivers"></a>AV/C クライアント ドライバー





Microsoft では、Windows XP およびそれ以降のオペレーティング システムで IEEE オーディオ/ビデオ コントロール (AV/C) プロトコルのサポートを提供します。 AV/C プロトコルでは、AV/C に準拠したデバイスに発行元のコマンドと応答の送信先をサブユニットからメソッドを定義します。 サブユニット ハードウェアをサポートするドライバーを作成する場合は、IEEE 1394 シリアル バス間で、AV/C プロトコルに準拠するデバイスでのサブユニットを制御できます。 Microsoft は、この機能では、その他の 2 つのドライバーを提供しているために、テープのサブユニットをサポートするためにサブユニット ドライバーを作成する必要がないことに注意してください*Msdv.sys*と*Mstape.sys*します。

AV/C プロトコルをサポートするためには、Microsoft は、次の 2 つのドライバーを提供します。

-   *Avc.sys*

-   *Avcstrm.sys*

*Avc.sys*は接続を確立し、管理のサブユニット/ユニットのサポートを提供する関数ドライバー。 *Avcstrm.sys*低いフィルター ドライバーに役立つ次の特定のデータ形式のストリーミング サポートを追加するには。

-   標準解像度デジタル ビデオ (SDDV 61883 2 の仕様)

-   MPEG2 TS (61883 4 の仕様)

提供されるオプションのサポートを使用するデバイスの機能、に応じて*Avcstrm.sys* SDDV や MPEG2 TS のデータのストリーミングを支援します。 場合*Avcstrm.sys* 、接続管理とデータのストリーミングによって公開される機能を使用して、デバイスで使用される形式はサポートされません*61883.sys*、下にあるドライバースタックです。

サブユニット ドライバーが従う必要があります、 [Windows Driver Model](https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-driver-model) (WDM) アーキテクチャ。 サブユニット ドライバーには、Stream クラス インターフェイスまたは AVStream インターフェイスを使用できます。 AVStream は、サブユニット ドライバーを開発するための推奨されるインターフェイスです。 Stream クラスのインターフェイスは廃止されていますと Microsoft は、さらに開発を廃止します。 これら 2 つのインターフェイスの詳細については、次を参照してください。 [AV/C カーネル ストリーミング インターフェイスと KS プロキシ プラグイン](av-c-kernel-streaming-interface-and-kernel-streaming-proxy-plug-ins.md)します。

AV/C のサブユニット ドライバーを作成する方法の詳細については、次を参照してください。 [AV/C 概要](av-c-overview.md)します。 使用する方法の詳細についての*Avcstrm.sys*ストリーミング データを支援するために、次を参照してください。 [/C AV ストリーミングの概要](av-c-streaming-overview.md)します。

AV/C のプロトコルのサポートは、IEEE 1394 のドライバー スタックおよび IEC 61883 標準に基づいて構築されます。 IEC 61883 ドライバー スタックの詳細については、次を参照してください。 [IEC 61883 クライアント ドライバー](https://docs.microsoft.com/windows-hardware/drivers/ieee/iec-61883-client-drivers)します。

 

 




