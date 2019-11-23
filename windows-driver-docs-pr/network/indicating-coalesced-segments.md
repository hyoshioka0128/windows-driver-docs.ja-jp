---
title: 結合されたセグメントの表示
description: このセクションでは、結合されるセグメントを指定する方法について説明します。
ms.assetid: 79A37DAB-D9B3-4FA2-8258-05E10BD6E3CB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed232fca02ada29091367011c92376d44f2335d9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824723"
---
# <a name="indicating-coalesced-segments"></a>結合されたセグメントの表示


1つの結合された単位 (SCU) は、tcp/ip[セグメントを結合するための規則](rules-for-coalescing-tcp-ip-packets.md)で定義されている規則に従って1つの tcp セグメントに結合される一連の tcp セグメントです。 このセクションでは、結合されたセグメントを示す方法について説明します。

SCU には次のものが必要です。

-   [**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)を呼び出すことによって示されます。

-   ネットワーク経由で受信される通常の TCP セグメントのように見えます。

-   [RFC 791](http://www.ietf.org/rfc/rfc791.txt)のセクション3.1 で定義されているように、有効な IP データグラムの最大長を超えることはできません。

    **注**  ipv6 拡張ヘッダーを持つセグメントは結合できないため (「[結合を終了する例外条件](exception-conditions-that-terminate-coalescing.md)」を参照)、IPV6 データグラムの scu のサイズも、有効なデータグラムの最大長によって制限されます。

     

NIC またはミニポートドライバーは、結合されたセグメントを示す前に、該当する場合は TCP および IPv4 チェックサムを再計算する必要があります。 NIC またはミニポートドライバーが TCP および IPv4 チェックサムを検証しても、結合されたセグメントの再計算が行われない場合は、 [**NDIS\_TCP\_IP\_チェックサム\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_ip_checksum_net_buffer_list_info)構造体の**TcpChecksumValueInvalid**フラグと**IpChecksumValueInvalid**フラグを設定する必要があります。 また、この場合、NIC またはミニポートドライバーでは、必要に応じて、セグメント内の TCP および IPv4 ヘッダーのチェックサム値をゼロにすることができます。

NIC とミニポートドライバーは、必ず、 [**NDIS\_TCP\_IP\_CHECKSUM\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_ip_checksum_net_buffer_list_info)構造体**のフラグを** **設定して**から、結合されたセグメントを示す必要があります。

結合規則の詳細については、「 [Tcp/ip セグメントを結合するための規則](rules-for-coalescing-tcp-ip-packets.md)」を参照してください。

例外の詳細については、「[合体を終了する例外条件](exception-conditions-that-terminate-coalescing.md)」を参照してください。

結合は、ベストエフォート方式で実行されることが想定されています。 リソースが不足しているなどの原因で、ハードウェアが合体できない場合があります。 ここでは、結合しない場合と結合する方法を指定するための要件について説明します。

大まかに言えば、NIC とミニポートドライバーは、次のようにネットワーク経由での TCP セグメントの受信を処理する必要があります。

-   次のようにして、受信セグメントで例外を確認します。

    1.  例外が検出されなかった場合は、規則に従って、同じ TCP 接続で受信した最後のセグメントでセグメントを結合できるかどうかを確認します。

    2.  セグメントが例外をトリガーした場合、または以前に受信したセグメントと結合できない場合は、セグメントを個別に指定します。

-   「 [Rsc の状態の照会と変更](querying-and-changing-rsc-state.md)」の説明に従って、プロトコルドライバーによって rsc が有効になるまで、NIC とミニポートドライバーは、結合されたセグメントを示すことはできません。

-   特定の TCP 接続の場合、ミニポートアダプターからホスト TCP/IP スタックへのデータ表示は、1つまたは複数の結合セグメントで構成されている可能性があります。これは、1つまたは複数の個別のセグメントによって分割されます。

-   NIC とミニポートドライバーは、結合されているかどうかにかかわらず、TCP セグメントを示す値を遅延させないようにする必要があります。 具体的には、NIC とミニポートドライバーは、セグメントの結合を試行するために、1つの遅延プロシージャ呼び出し (DPC) から次のセグメントへのセグメントの通知を遅らせないようにする必要があります。

-   NIC とミニポートドライバーは、結合の終了を判断するためにタイマーを使用する場合があります。 ただし、待機時間に依存するワークロードの処理は、DPC の境界要件と同じように有効にする必要があります。

 

 





