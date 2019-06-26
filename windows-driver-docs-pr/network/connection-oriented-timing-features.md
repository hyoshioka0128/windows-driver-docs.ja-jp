---
title: 接続指向タイミング機能
description: 接続指向タイミング機能
ms.assetid: 73b005c2-39bd-4931-89cd-7ea3db9068ca
keywords:
- 接続指向 NDIS WDK、タイミングの機能
- いる CoNDIS WDK ネットワーク、機能のタイミング
- タイミング機能 WDK いる CoNDIS
- クロック
- ローカル クロック WDK いる CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c3548eedcf292016591251735b19fcc6dd1560c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374947"
---
# <a name="connection-oriented-timing-features"></a>接続指向タイミング機能





パケットの送信のスケジュールとタイムスタンプは、NIC のローカル時刻を使用して、接続指向 NDIS サポートは、パケットを送受信します。

**注**  これらタイミングの接続指向の機能は省略可能です。 これらの機能はすべている CoNDIS Nic でサポートされていません。

 

接続指向プロトコル ドライバーに呼び出せる[ **NdisCoOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscooidrequest)で MCM、接続指向のミニポート ドライバーのローカルのタイミングの機能を照会する[OID\_GEN\_CO\_取得\_時間\_CAP](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-co-get-time-caps)します。 このようなクエリに応答してでミニポート ドライバーまたは MCM ドライバーはに関する情報を返します。

-   NIC で読み取り可能なクロックがあるかどうか

-   かどうか、NIC は、ネットワーク接続から、時間を取得します。

-   ローカル クロックの有効桁数。

-   NIC にタイムスタンプができるかどうかのローカル時刻でのパケットを受信しました。

-   かどうか、NIC には、そのローカル時刻に従って伝送の送信パケットをスケジュールできます。

-   NIC にタイムスタンプができるかどうかと、そのローカル時刻を持つパケットが送信されます。

NIC のローカル時刻を取得する接続指向プロトコルを呼び出すことができます**NdisCoOidRequest**接続指向のミニポート ドライバーまたは MCM のドライバーの照会に[OID\_GEN\_CO\_取得\_ネットワーク カード\_時間](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-co-get-netcard-time)します。 接続指向のミニポート ドライバーまたは MCM ドライバーは同期的にパケットの転送をスケジュールする接続指向プロトコルを使用できますし、ローカル時刻を取得するを返します。

タイミング情報を送信または受信パケットが、パケットのアウト オブ バンド (OOB) データに含まれています。 詳細については、次を参照してください。 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)します。

 

 





