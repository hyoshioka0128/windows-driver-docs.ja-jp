---
title: IPsec Offload Version 2 によるネットワーク データの受信
description: IPsec Offload Version 2 によるネットワーク データの受信
ms.assetid: c09ce374-6dd6-4d16-914b-5576304d4440
keywords:
- IPsecOV2 WDK TCP/IP トランスポートは、データの受信
- 受信側のデータの WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: afb3fd2b59f2fd4a4b22f47ee0865f3bd2952447
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353297"
---
# <a name="receiving-network-data-with-ipsec-offload-version-2"></a>IPsec Offload Version 2 によるネットワーク データの受信

\[IPsec タスク オフロード機能は非推奨し、は使用できません。\]




NIC は、IPsec オフロード バージョン 2 (IPsecOV2)、トランスポートからオフロードされたセキュリティ アソシエーション (SA) で指定された受信パケットの処理を実行します。

ミニポート ドライバーでは、上にあるドライバーを受信したデータを示す前に、IPsecOV2 帯域外の (OOB) 情報を設定します。 OOB の情報にアクセスする方法の詳細については、次を参照してください。[にアクセスする NET\_バッファー\_一覧については、IPsec オフロード バージョン 2 で](accessing-net-buffer-list-information-in-ipsec-offload-version-2.md)します。

**注**  ミニポート ドライバーは、NIC で IPsec データの処理中にエラーが発生した場合でも、ドライバーを関連するすべての受信パケットを示す必要があります ドライバーは、パケットを監視し、ネットワーク トラフィックのトラブルシューティングを行うドライバー スタックを有効にエラーを示す必要があります。

 

ミニポートする前に、ドライバーはドライバー スタック、ミニポート ドライバーを受信したデータ パケットを示します。

-   IPsec オフロード タスクを処理するために、ハードウェアが構成されていることを確認します。 ミニポート ドライバーのないその他の IPsec で受信 indication はそうでない場合は、処理をオフロードします。

-   セキュリティ パラメーター インデックス (SPI) かどうかは、SA をオフロード、一致するかを判断するには存在します。 パケットの宛先アドレスは、1 つで指定したオフロード SA と同じ、ミニポート ドライバーを確認します。 一致する SA がない場合は、NIC を IPsecOV2 OOB 情報を設定せず、受信したデータを示します。

-   ミニポート ドライバーは、トランスポートに報告する機能に基づいて、パケットを処理できるか、さらに IPsec の処理を行わなくても、受信を示す値になることを確認します。 たとえば、パケットは IP オプションで、NIC がこのようなパケットを処理する IPsec オフロードをサポートしていませんし、ミニポート ドライバーは、IPsec の処理があります。

-   セット、 **CryptoDone**フラグ、 [ **NDIS\_IPSEC\_オフロード\_V2\_NET\_バッファー\_一覧\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_ipsec_offload_v2_net_buffer_list_info)構造体を NIC が IPsec で受信したパケットの少なくとも 1 つの IPsec ペイロードでチェックを実行することを示します。

-   セット、 **NextCryptoDone** NDIS フラグ\_IPSEC\_オフロード\_V2\_NET\_バッファー\_一覧\_を示すために、情報構造体NIC は IPsec 受信パケットのトンネルおよびトランスポートの両方の部分でチェックを実行します。 ミニポート ドライバーがパケットにトンネルおよびトランスポートの両方のペイロードがある場合にのみ、このフラグを設定します。それ以外の場合、このフラグは 0 にする必要があります。

-   適切な設定**CryptoStatus** NDIS の値\_IPSEC\_オフロード\_V2\_NET\_バッファー\_一覧\_情報構造体IPsec チェックの結果を示します。

ミニポート ドライバーが両方をクリアして、NIC でオフロードが着信パケットの処理が実行されなかった場合、 **CryptoDone**と**NextCryptoDone**フラグ。 ミニポート ドライバーのクリア、NIC 解読されません、パケットは、AH または ESP で保護されているかどうかに関係なくパケットの受信のすべてのこれらのフラグ。

ミニポート ドライバーを設定できます**SaDeleteReq**の[ **NDIS\_IPSEC\_オフロード\_V2\_NET\_バッファー\_一覧\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_ipsec_offload_v2_net_buffer_list_info)受信構造[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)します。 TCP/IP トランスポートは発行後[OID\_TCP\_タスク\_IPSEC\_オフロード\_V2\_削除\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-delete-sa)を削除する 1 回、受信パケットの受信に使用された SA とに 1 回もう一度削除済みに対応する送信の SA を削除するのには、SA を受信します。 追加と削除の SAs の詳細については、次を参照してください。 [IPsec オフロード バージョン 2 のセキュリティ アソシエーションを管理する](managing-security-associations-in-ipsec-offload-version-2.md)します。

ミニポート後は、ドライバーは、NET を示します\_バッファー\_リスト構造を TCP/IP トランスポートに TCP/IP トランスポートは、パケットの場合、シーケンス番号のチェック、NIC が、パケットに対して IPsec チェックの結果を調べます。チェックサムまたはテストをシーケンス処理に失敗したパケットの処理を決定します。

 

 





