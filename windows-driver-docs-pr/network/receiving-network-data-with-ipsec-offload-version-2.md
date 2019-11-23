---
title: IPsec Offload Version 2 によるネットワーク データの受信
description: IPsec Offload Version 2 によるネットワーク データの受信
ms.assetid: c09ce374-6dd6-4d16-914b-5576304d4440
keywords:
- IPsecOV2 WDK TCP/IP トランスポート、受信データ
- データを受信する WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f19d05125db068aa2ac997f96f0d47f314bcd36
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843465"
---
# <a name="receiving-network-data-with-ipsec-offload-version-2"></a>IPsec Offload Version 2 によるネットワーク データの受信

\[IPsec タスクオフロード機能は非推奨とされているため、使用しないでください。\]




NIC は、トランスポートからオフロードされたセキュリティアソシエーション (SA) で指定されているように、受信パケットで IPsec オフロードバージョン 2 (IPsecOV2) 処理を実行します。

ミニポートドライバーは、IPsecOV2 帯域外 (OOB) 情報を設定してから、そのドライバーに受信したデータを示します。 OOB 情報へのアクセスの詳細については、「 [IPsec オフロードバージョン2での NET\_BUFFER\_LIST 情報へのアクセス](accessing-net-buffer-list-information-in-ipsec-offload-version-2.md)」を参照してください。

ミニポートドライバーは、NIC 内の IPsec データの処理中にエラーが発生した場合でも、すべての受信パケットをそれまでのドライバーに対して示す必要がある  に**注意**してください。 ドライバーは、ドライバースタックでネットワークトラフィックの監視とトラブルシューティングを行うために、エラーのあるパケットを示す必要があります。

 

ミニポートドライバーは、受信したデータパケットがドライバースタックの上にあることを示す前に、次のようにします。

-   ハードウェアが IPsec オフロードタスクを処理するように構成されていることを確認します。 それ以外の場合、ミニポートドライバーは、追加の IPsec オフロード処理を行わずに受信を示します。

-   は、セキュリティパラメーターインデックス (SPI) を調べて、一致するオフロード SA が存在するかどうかを確認します。 ミニポートドライバーは、パケットの宛先アドレスがオフロード SA に指定されているアドレスと同じであることを確認します。 一致する SA がない場合、NIC は IPsecOV2 OOB 情報を設定せずに受信したデータを示します。

-   ミニポートドライバーによってトランスポートに報告された機能に基づいてパケットを処理できることを確認します。それ以外の場合は、IPsec 処理を行わずに受信を通知します。 たとえば、パケットには IP オプションがあり、NIC はこのようなパケットの IPsec オフロード処理をサポートしておらず、ミニポートドライバーは IPsec 処理を実行します。

-   [**NDIS\_ipsec\_オフロード\_V2\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_net_buffer_list_info)構造体の**cryptodone**フラグを設定して、NIC が受信パケット内の少なくとも1つの ipsec ペイロードに対して ipsec チェックを実行したことを示します。

-   NDIS\_IPSEC\_オフロード\_V2\_NET\_BUFFER\_LIST\_INFO 構造体の**Nextcryptodone**フラグを設定して、NIC が受信パケットのトンネルとトランスポートの両方の部分に対して ipsec チェックを実行したことを示します。 このフラグは、パケットにトンネルペイロードとトランスポートペイロードの両方がある場合にのみ、このフラグを設定します。それ以外の場合、このフラグは0にする必要があります。

-   Ipsec チェックの結果を示すために、NDIS\_IPSEC\_オフロード\_V2\_NET\_BUFFER\_LIST\_INFO 構造体の正しい**Cryptostatus**値を設定します。

NIC が受信パケットでオフロード処理を実行しなかった場合、ミニポートドライバーは、 **cryptodone**フラグと**nextcryptodone**フラグの両方をクリアします。 ミニポートドライバーは、パケットが AH で保護されているか、または ESP で保護されているかに関係なく、NIC が暗号化を解除しないすべての受信パケットに対してこれらのフラグをクリアします。

ミニポートドライバーは、 **SaDeleteReq**を設定できます。そのためには、 [**NDIS\_IPSEC\_オフロード\_V2\_net\_buffer\_list\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_net_buffer_list_info)構造体を受信[**net\_buffer\_list**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)に使用します。 その後、TCP/IP トランスポートは[\_tcp\_タスク\_IPSEC\_オフロード\_V2\_\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-delete-sa)を一度削除してパケットを受信した受信 sa を一度削除し、削除された受信 sa に対応する送信 sa を削除します。 SAs の追加と削除の詳細については、「 [IPsec オフロードバージョン2でのセキュリティアソシエーションの管理](managing-security-associations-in-ipsec-offload-version-2.md)」を参照してください。

ミニポートドライバーによって、ネットワーク\_バッファー\_一覧構造が TCP/IP トランスポートに対して示された後、TCP/IP トランスポートは、パケットで実行された NIC による IPsec チェックの結果を調べ、パケットのシーケンス番号を確認し、チェックサムまたはシーケンステストに失敗したパケットの処理を決定します。

 

 





