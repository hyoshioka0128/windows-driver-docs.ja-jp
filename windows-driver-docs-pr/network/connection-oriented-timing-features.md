---
title: 接続指向のタイミング機能
description: 接続指向のタイミング機能
ms.assetid: 73b005c2-39bd-4931-89cd-7ea3db9068ca
keywords:
- 接続指向の NDIS WDK、タイミング機能
- Condwdk ネットワーク、タイミング機能
- タイミング機能 (WDK の場合)
- 時計
- ローカルクロック WDK CoNDIS 場合
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 011fe81f1518d201e41a896ff85eeb64972108b1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838177"
---
# <a name="connection-oriented-timing-features"></a>接続指向のタイミング機能





接続指向 NDIS では、NIC のローカル時刻を使用してパケットの送信をスケジュールしたり、パケットの送信と受信のタイムスタンプを設定したりできます。

**ただし**、これらの接続指向のタイミング機能は省略可能  ます。 これらの機能は、すべての CoNDIS でサポートされているわけではありません。

 

接続指向のプロトコルドライバーは、 [**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest)を呼び出すことで、接続指向ミニポートドライバーまたは mcm ドライバーのローカルタイミング機能に対してクエリを実行できます。 [OID\_GEN\_CO\_GET\_TIME\_CAPS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-co-get-time-caps). このようなクエリに応答して、ミニポートドライバーまたは MCM ドライバーは次の情報を返します。

-   NIC に読み取り可能なクロックがあるかどうか。

-   NIC がネットワーク接続から時間を取得するかどうか。

-   ローカルクロックの有効桁数。

-   NIC がローカル時刻を使用して受信パケットのタイムスタンプを行うことができるかどうか。

-   NIC がローカル時刻に従って送信パケットを送信するようにスケジュールできるかどうかを指定します。

-   NIC がローカル時刻で送信されたパケットにタイムスタンプを付けられるかどうかを指定します。

NIC のローカル時刻を取得するために、接続指向のプロトコルは**NdisCoOidRequest**を呼び出して、接続指向のミニポートドライバーまたは OID\_GEN を使用した mcm ドライバーに対してクエリを実行し、 [\_のネットカード\_時刻を\_CO\_取得](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-co-get-netcard-time)します。 接続指向ミニポートドライバーまたは MCM ドライバーは、同期的にローカル時刻を返します。これにより、接続指向のプロトコルは、パケットの送信をスケジュールするために使用できます。

送信または受信パケットのタイミング情報は、パケットの帯域外 (OOB) データに含まれています。 詳細については、「 [**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)」を参照してください。

 

 





