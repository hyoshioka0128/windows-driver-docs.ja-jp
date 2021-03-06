---
title: 結合されたセグメントの表示
description: このセクションは、まとめられたセグメントを指定する方法を説明します
ms.assetid: 79A37DAB-D9B3-4FA2-8258-05E10BD6E3CB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be13f521a54a65da4942868bb7331321993471f8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374828"
---
# <a name="indicating-coalesced-segments"></a>結合されたセグメントの表示


1 つのまとめられた単位 (SCU) で定義されたルールに従って 1 つの TCP セグメントとして結合 TCP セグメントのシーケンスは、 [TCP/IP セグメントの結合規則](rules-for-coalescing-tcp-ip-packets.md)します。 このセクションでは、結果として得られるまとめられたセグメントを指定する方法について説明します。

SCU 必要があります。

-   呼び出すことによって示される[ **NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatereceivenetbufferlists)します。

-   通常、ネットワーク経由で受信された TCP セグメントのようになります。

-   セクション 3.1 で定義されている有効な最大の IP データグラム長を超えるする[RFC 791](http://www.ietf.org/rfc/rfc791.txt)します。

    **注**  IPv6 拡張ヘッダーを持つセグメントを結合できないため、(を参照してください[例外条件がその終了結合](exception-conditions-that-terminate-coalescing.md))、IPv6 データグラム SCU のサイズ、最大の法律によって制限されますデータグラムの長さ。

     

NIC またはミニポート ドライバーする必要があります値を再計算と IPv4 の TCP チェックサム、該当する場合、まとめられたセグメントを示す前にします。 NIC またはミニポート ドライバーでは、TCP と IPv4 のチェックサムを検証しますが、まとめられたセグメントの再計算してされない場合に、設定する必要があります、 **TcpChecksumValueInvalid**と**IpChecksumValueInvalid**のフラグ[ **NDIS\_TCP\_IP\_チェックサム\_NET\_バッファー\_一覧\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_tcp_ip_checksum_net_buffer_list_info)構造体。 さらに、この場合、NIC またはミニポート ドライバー可能性があります必要に応じてをゼロに TCP と IPv4 ヘッダーのチェックサム値セグメント。

NIC とミニポート ドライバーが常に設定する必要があります、 **IpChecksumSucceeded**と**TcpChecksumSucceeded**のフラグ、 [ **NDIS\_TCP\_IP\_チェックサム\_NET\_バッファー\_一覧\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_tcp_ip_checksum_net_buffer_list_info)まとめられたセグメントを示す前に構造体。

結合規則の詳細については、次を参照してください。 [TCP/IP セグメントの結合規則](rules-for-coalescing-tcp-ip-packets.md)します。

例外の詳細については、次を参照してください。[例外条件がその終了結合](exception-conditions-that-terminate-coalescing.md)します。

ベスト エフォートで実行する結合が必要です。 ハードウェアが、coalesce では、場合によっては、たとえばによりリソースの不足ができません。 要件は、ここでは、主に coalesce をしない場合と結合する方法を指定すると述べています。

大まかに言えば、NIC とミニポート ドライバーする必要があります TCP セグメントの受信、ネットワーク経由でよう処理。

-   次のように、例外の受信のセグメントを確認します。

    1.  例外が発生しなかった場合は、規則に従って同じ TCP 接続を受信した最後のセグメントのセグメントを結合しているかどうかを確認します。

    2.  セグメントには、例外がトリガーされた場合、または、以前に受信したセグメントでの結合が不可能な場合は、セグメントを個別に示すします。

-   プロトコル ドライバーが」の説明に従って、RSC を有効になるまで、NIC とミニポート ドライバーする必要がありますまとめられたセグメントを示しません[クエリの実行と RSC の状態を変更する](querying-and-changing-rsc-state.md)します。

-   特定の TCP 接続のホストの TCP/IP スタックにミニポート アダプターからのデータ表示が 1 つまたは複数結合されたセグメントの結合されたいない 1 つまたは複数の個別セグメントで区切られたで構成されます。

-   ひとまとめにするかどうかどうか、NIC とミニポート ドライバーは、TCP セグメントを示す値を遅延しない必要があります。 具体的には、NIC とミニポート ドライバーでは、1 つの遅延プロシージャ呼び出し (DPC) をセグメントを結合するために、次のセグメントを示す値が遅延しない必要があります。

-   NIC とミニポート ドライバーは、結合の末尾を決定するのにタイマーを使用する場合があります。 ただし、待機時間の機密性の高いワークロードの処理は、DPC 境界の要件として効果的である必要があります。

 

 





