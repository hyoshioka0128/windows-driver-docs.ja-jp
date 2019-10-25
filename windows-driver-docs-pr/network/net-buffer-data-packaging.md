---
title: NET_BUFFER データのパッケージ化
description: NET_BUFFER データのパッケージ化
ms.assetid: f0d539ab-c6ed-4cd9-9891-ef4235016d50
keywords:
- NDIS WDK、送受信 (データを)
- データパッケージ WDK ネットワーク
- データの送信 (WDK ネットワーク)
- データを受信する WDK ネットワーク
- NDIS_PACKET
- NET_BUFFER データパッケージの WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a33ddb5c21b601d255f9897e2a99dbd9ee7aced
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844929"
---
# <a name="net_buffer-data-packaging"></a>NET\_バッファーデータのパッケージ化





データパッケージは、NDIS 6.0 で再設計されました。 [**NDIS\_パケット**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff557086(v=vs.85))構造に基づく送信および受信アーキテクチャは、 [**net\_buffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)と[**net\_buffer\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造に基づくアーキテクチャに置き換えられました。 NET\_のバッファー構造は、NDIS\_パケット構造に相当する機能です。 NET\_のバッファー構造では、ネットワークデータ用のバッファー (MDL チェーン) と、NDIS、プロトコルドライバー、およびミニポートドライバー用の予約領域を指定します。 Net\_BUFFER\_LIST 構造体で記述されているリスト内で、NET\_バッファー構造をリンクすることができます。 また、NET\_BUFFER\_LIST 構造体は、一覧内のすべての NET\_バッファー構造に適用される帯域外 (OOB) データ用のストレージも提供します。

Microsoft 次世代ネットワークドライバースタック内のすべてのコンポーネント (TCP/IP トランスポートと Winsock を含む) は、NET\_のバッファーデータのパッケージ化を使用します。 ドライバースタック全体にわたって一様にデータをパッケージ化することで、データの再パッケージ化、データ処理の簡素化、および関数呼び出しの回数の削減が実現されます。

Ndis\_パケット構造を使用する古いドライバーに対応するために、ndis 6.0 は NDIS\_パケット構造を NET\_バッファー構造に変換します。 この翻訳は、NDIS ドライバーに対して透過的です。

NDIS は、ドライバーのデータバックフィル要件を上位レベルのドライバーに伝達します。 NET\_BUFFER と NET\_BUFFER を割り当ててデータを送信するために\_リスト構造を割り当てる場合、上位レベルのドライバーはスタック内のすべての下位レベルのドライバーを格納するために十分なデータ領域を割り当てます。 そのため、下位レベルのドライバーでは、レイヤー固有のヘッダーを格納するために追加のバッファー領域を割り当てる必要はありません。 代わりに、事前に割り当てられたバックフィル領域を使用できます。

NET\_のバッファーアーキテクチャの詳細については、「 [net\_バッファーアーキテクチャ](net-buffer-architecture.md)」を参照してください。

 

 





