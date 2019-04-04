---
title: AV/C クライアント ドライバー
description: AV/C クライアント ドライバー
ms.assetid: 70d98c31-2da6-455b-91d8-59bed306b574
keywords:
- AVStream WDK、AV/C
- AV/C WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f5dfa74d7f2b1a9229e23579d29c8f950ac43ea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557473"
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

サブユニット ドライバーが従う必要があります、 [Windows Driver Model](https://msdn.microsoft.com/library/windows/hardware/ff565698) (WDM) アーキテクチャ。 サブユニット ドライバーには、Stream クラス インターフェイスまたは AVStream インターフェイスを使用できます。 AVStream は、サブユニット ドライバーを開発するための推奨されるインターフェイスです。 Stream クラスのインターフェイスは廃止されていますと Microsoft は、さらに開発を廃止します。 これら 2 つのインターフェイスの詳細については、[AV/C カーネル ストリーミング インターフェイスと KS プロキシ プラグイン](av-c-kernel-streaming-interface-and-kernel-streaming-proxy-plug-ins.md)を参照してください。

AV/C のサブユニット ドライバーを作成する方法の詳細については、[AV/C 概要](av-c-overview.md)を参照してください。 使用する方法の詳細についての*Avcstrm.sys*ストリーミング データを支援するために、[/C AV ストリーミングの概要](av-c-streaming-overview.md)を参照してください。

AV/C のプロトコルのサポートは、IEEE 1394 のドライバー スタックおよび IEC 61883 標準に基づいて構築されます。 IEC 61883 ドライバー スタックの詳細については、[IEC 61883 クライアント ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff537188)を参照してください。

 

 




