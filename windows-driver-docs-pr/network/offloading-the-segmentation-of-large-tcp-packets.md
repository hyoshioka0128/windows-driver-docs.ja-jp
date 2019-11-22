---
title: 大きな TCP パケットのセグメント化のオフロード
description: 大きな TCP パケットのセグメント化のオフロード
ms.assetid: 6ae162fb-a8fc-47b8-80ae-ff39f3059d53
keywords:
- タスクオフロード WDK TCP/IP トランスポート、大きなパケットセグメント化
- 大きな TCP パケットセグメント化 WDK ネットワーク
- 大きな TCP パケットのセグメンテーション (WDK ネットワーク)
ms.date: 10/24/2019
ms.localizationpriority: medium
ms.openlocfilehash: ae71234073c62c3ba9f5987e6b300ddf6028a285
ms.sourcegitcommit: 0660c8d6d374298f3246fdb91661360610f8c846
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72889648"
---
# <a name="offloading-the-segmentation-of-large-tcp-packets"></a>大きな TCP パケットのセグメント化のオフロード

NDIS ミニポートドライバーを使用すると、ネットワークメディアの最大転送単位 (MTU) を超える大きな TCP パケットのセグメント化をオフロードできます。 大きな TCP パケットのセグメント化をサポートする NIC も、次のことを可能にする必要があります。

-   IP オプションを含む送信パケットの IP チェックサムを計算します。

-   TCP オプションを含む送信パケットの TCP チェックサムを計算します。

NDIS バージョン6.0 以降では、NDIS 5 の large send offload (LSO) に似た large send offload version 1 (LSOv1) がサポートされています。*x*。 また、NDIS バージョン6.0 以降では、大規模な送信オフロードバージョン 2 (LSOv2) もサポートされています。これは、IPv6 のサポートなど、拡張された大きなパケットセグメンテーションサービスを提供します。

LSOv2 と LSOv1 をサポートするミニポートドライバーでは、 [**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) structure OOB information のオフロードの種類を決定する必要があります。 ドライバーは、NDIS の**Type**メンバー [ **\_TCP\_LARGE\_SEND\_オフロード\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_large_send_offload_net_buffer_list_info)構造体を使用して、ドライバースタックが LSOv2 または LSOv1 を使用しているかどうかを判断できます。適切なオフロードサービスを実行します。 LSOv1 または LSOv2 OOB データを含むすべての NET\_BUFFER\_LIST 構造には、1つの[**net\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造も含まれています。 NDIS\_TCP\_LARGE\_送信\_オフロード\_NET\_BUFFER\_\_情報については、「 [Tcp/ip オフロード NET\_buffer\_List information](accessing-tcp-ip-offload-net-buffer-list-information.md)」を参照してください。

ただし、ミニポートで[ **\_TCP\_オフロード\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-parameters)を使用して、ミニポートで LSO 機能を無効にし、ミニポートが oid を正常に完了した後、ミニポートは、0以外の LSOv1 または LSOv2 OOB データを含むすべての[**net\_BUFFER\_list**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)をドロップします ([**NDIS\_TCP\_LARGE\_送信\_オフロード\_net\_BUFFER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_large_send_offload_net_buffer_list_info)\_\_ 

TCP/IP トランスポートは、次の条件を満たすサイズの大きい TCP パケットのみをオフロードします。

-   パケットは TCP パケットです。 TCP/IP トランスポートでは、セグメント化のために大きな UDP パケットの負荷が軽減されません。

-   パケットは、少なくともミニポートドライバーによって指定されたセグメントの最小数で割り切れなければなりません。 詳細については、「 [nic の LSOv1 機能の報告](reporting-a-nic-s-lsov1-tcp-packet-segmentation-capabilities.md)」および「 [nic の LSOv2 の tcp パケットセグメント化機能の報告](reporting-a-nic-s-lsov2-tcp-packet-segmentation-capabilities.md)」を参照してください。

-   パケットがループバックパケットではありません。

-   パケットはトンネル経由で送信されません。

大きな TCP パケットのセグメント化をオフロードする前に、TCP/IP トランスポートは次のようになります。

-   [**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造に関連付けられている大量のパケットセグメンテーション情報を更新します。 この情報は、 [**NDIS\_TCP\_LARGE\_送信\_オフロード\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_large_send_offload_net_buffer_list_info) net **\_buffer\_** list\_INFO 構造体に含まれています。**NET\_BUFFER\_LIST**構造体に関連付けられています。\_\_ **Net\_buffer\_リスト**の詳細については、「 [TCP/IP オフロード net\_Buffer\_list information](accessing-tcp-ip-offload-net-buffer-list-information.md)」を参照してください。 TCP/IP トランスポートは、 **mss**値を最大セグメントサイズ (mss) に設定します。

<a name="lsov1lengthrequirements"></a>

- LSOv1 の場合は、サイズの大きい TCP パケットの合計長をパケットの IP ヘッダーの合計長フィールドに書き込みます。 合計の長さには、IP ヘッダーの長さ、IP オプションが存在する場合はその長さ、TCP ヘッダーの長さ、tcp オプションが存在する場合はその長さ、tcp ペイロードの長さが含まれます。 LSOv2 の場合、パケットの IP ヘッダーの [合計長] フィールドを0に設定します。 ミニポートドライバーは、NET_BUFFER_LIST 構造の最初の NET_BUFFER 構造の長さからパケットの長さを決定する必要があります。

-   TCP 擬似ヘッダーの1の補数の合計を計算し、この合計を TCP ヘッダーのチェックサムフィールドに書き込みます。 TCP/IP トランスポートは、擬似ヘッダー内の次のフィールドに対する1の補数の合計を計算します。発信元 IP アドレス、宛先 IP アドレス、およびプロトコルです。 TCP/IP トランスポートによって提供される疑似ヘッダーの1の補数和により、NIC は、IP ヘッダーを調べることなく、大きな TCP パケットから取得した各パケットの実際の TCP チェックサムの計算を初期段階で開始します。 RFC 793 では、ソース IP アドレス、宛先 IP アドレス、プロトコル、および TCP の長さに対して擬似ヘッダーチェックサムが計算されることを明記されしています。 (TCP の長さは tcp ヘッダーの長さに、TCP ペイロードの長さを加えたものです。 TCP の長さには、擬似ヘッダーの長さは含まれません)。ただし、基になるミニポートドライバーと NIC は、tcp/ip トランスポートによって渡される大きなパケットから TCP セグメントを生成するため、トランスポートは各 TCP セグメントの TCP ペイロードのサイズを認識しないため、TCP の長さを含めることはできません。擬似ヘッダー。 代わりに、次に示すように、NIC は、生成された各 TCP セグメントの TCP の長さに対応するために TCP/IP トランスポートによって提供された擬似ヘッダーチェックサムを拡張します。

-   TCP ヘッダーのシーケンス番号フィールドに正しいシーケンス番号を書き込みます。 シーケンス番号は、TCP ペイロードの最初のバイトを識別します。

ミニポートドライバーは、 [*Miniportsendnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists)関数または[**Miniportcosendnetbufferlists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_send_net_buffer_lists)関数内の[**net\_buffer\_list**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体を取得した後、 **TcpLargeSendNetBufferListInfo**の *\_ID*を使用して[**NET\_buffer\_list\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-info)マクロを呼び出し、tcp/ip トランスポートによって書き込まれた MSS 値を取得できます。

ミニポートドライバーは、パケットの IP ヘッダーから大きなパケットの合計長を取得し、MSS 値を使用して大きな TCP パケットを小さいパケットに分割します。 小さいパケットには、MSS 以下のユーザーデータバイトが含まれます。 セグメント化された大きいパケットから作成された最後のパケットのみが、MSS ユーザーデータバイト未満であることに注意してください。 セグメント化されたパケットから作成された他のすべてのパケットには、MSS ユーザーデータバイトが含まれている必要があります。 この規則に従わないと、不要な余分なパケットの作成と送信によってパフォーマンスが低下する可能性があります。

ミニポートドライバーは、大きなパケットから派生した各セグメントに対して、MAC、IP、および TCP ヘッダーを接辞します。 ミニポートドライバーは、これらの派生パケットの IP および TCP チェックサムを計算する必要があります。 大きな TCP パケットから派生した各パケットの TCP チェックサムを計算するために、NIC は tcp チェックサムの可変部分 (TCP ヘッダーおよび TCP ペイロード用) を計算し、このチェックサムを、によって計算された擬似ヘッダーの1の補数合計に追加します。次に、TCP/IP トランスポートを使用して、チェックサムの16ビットの1の補数を計算します。 このようなチェックサムの計算の詳細については、RFC 793 および RFC 1122 を参照してください。

次の図は、大きなパケットのセグメント化を示しています。

![大きいパケットのセグメント化を示す図](images/segmentation.png)

大きな TCP パケット内の TCP ユーザーデータの長さは、ミニポートドライバーが**Maxoffloadsize**値に割り当てる値以下である必要があります。 **Maxoffloadsize**値の詳細については、「 [Nic の LSOv1 機能の報告](reporting-a-nic-s-lsov1-tcp-packet-segmentation-capabilities.md)」と「 [Nic の LSOv2 機能の報告](reporting-a-nic-s-lsov2-tcp-packet-segmentation-capabilities.md)」を参照してください。

ドライバーは、 **Maxoffloadsize**値が変更されたことを示すステータス情報を発行した後、前の**maxoffloadsize**値を使用する LSO 送信要求を受信した場合、ドライバーをクラッシュさせないようにする必要があります。 代わりに、ドライバーは送信要求を失敗させることができます。

**Maxoffloadsize**値が変更されたことを報告するステータス表示を個別に発行する中間ドライバーは、状態を表示していない、基になるミニポートアダプターがサイズの大きいパケットを取得していないことを確認する必要があります。ミニポートアダプターによって報告された**Maxoffloadsize**値を超えています。

[OID\_TCP\_オフロード\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-parameters)に応答するミニポート中間ドライバーでは、lso サービスを無効にするために、lso の送信要求がミニポートドライバーに到着する可能性がある小さな時間帯のために準備する必要があります。

セグメントパケット内の TCP ユーザーデータの長さは、MSS 以下である必要があります。 MSS は、[**ネットワーク\_バッファー\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造に関連付けられている、LSO NET\_BUFFER\_リスト情報を使用して、TCP トランスポートが通過する ULONG 値です。 セグメント化された大きいパケットから作成された最後のパケットのみが、MSS ユーザーデータバイト未満であることに注意してください。 セグメント化されたパケットから作成された他のすべてのパケットには、MSS ユーザーデータバイトが含まれている必要があります。 この規則に従わないと、不要な余分なパケットの作成と送信によってパフォーマンスが低下する可能性があります。

大きな TCP パケットから派生したセグメントパケットの数は、ミニポートドライバーによって指定された**MinSegmentCount**値以上である必要があります。 **MinSegmentCount**値の詳細については、「 [Nic の LSOv1 機能を報告する](reporting-a-nic-s-lsov1-tcp-packet-segmentation-capabilities.md)」および「 [Nic の LSOv2 TCP パケットセグメント化機能の報告](reporting-a-nic-s-lsov2-tcp-packet-segmentation-capabilities.md)」を参照してください。

次の前提条件と制限は、すべてのバージョンの LSO 対応ミニポートドライバーの IP ヘッダーと TCP ヘッダーを処理する場合に適用されます。

-   TCP/IP トランスポートオフロードが設定されていない、サイズの大きい TCP パケットの IP ヘッダーの MF ビット。 IP ヘッダー内のフラグメントオフセットはゼロになります。

-   Large TCP パケットの TCP ヘッダーに含まれる URG、RST、および SYN フラグは設定されず、TCP ヘッダーの緊急オフセット (ポインター) は0になります。

-   大きいパケットの TCP ヘッダー内の FIN ビットが設定されている場合、ミニポートドライバーは、大きな TCP パケットから作成された最後のパケットの TCP ヘッダーにこのビットを設定する必要があります。

-   Large TCP パケットの TCP ヘッダー内の PSH ビットが設定されている場合、ミニポートドライバーは、サイズの大きい TCP パケットから作成された最後のパケットの TCP ヘッダーにこのビットを設定する必要があります。

-   Large TCP パケットの TCP ヘッダーの CWR ビットが設定されている場合、ミニポートドライバーは、大きな TCP パケットから作成される最初のパケットの TCP ヘッダーにこのビットを設定する必要があります。 ミニポートドライバーは、大きな TCP パケットから作成した最後のパケットの TCP ヘッダーにこのビットを設定することができますが、これは望ましくありません。

-   大きい TCP パケットに IP オプションまたは TCP オプション (またはその両方) が含まれている場合、ミニポートドライバーは、これらのオプションを変更せずに、大きな TCP パケットから派生した各パケットにコピーします。 具体的には、NIC によってタイムスタンプオプションが増分されることはありません。

-   すべてのパケットヘッダー (イーサネット、IP、TCP) は、パケットの最初の MDL に配置されます。 ヘッダーは、複数の MDLs に分割されません。 
    > [!TIP]
    > この想定は、LSO が有効になっている場合に有効です。 それ以外の場合、LSO が有効になっていないと、ミニポートドライバーは、IP ヘッダーがイーサネットヘッダーと同じ MDL にあると想定できません。


ミニポートドライバーは、TCP/IP トランスポートから NET\_BUFFER\_リスト構造を受け取る順序で、 [**net\_buffer\_list**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体にパケットを送信する必要があります。

大きな TCP パケットを処理する場合、ミニポートアダプターはパケットをセグメント化し、付加の MAC、IP、および TCP ヘッダーを大きな TCP パケットから派生したパケットに分割します。 TCP/IP トランスポートは、他のすべてのタスク (リモートホストの受信ウィンドウサイズに基づいた送信ウィンドウサイズの調整など) を実行します。

[**NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)や[**NdisMCoSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcosendnetbufferlistscomplete)などの大規模なパケットの送信操作を完了する前に、ミニポートドライバーは、 [**NDIS\_\_tcp に書き込み\_オフロード\_オフロードの\_送信オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_large_send_offload_net_buffer_list_info)に使用されています。また、オフロードの場合は net\_バッファー\_リスト情報) を出力します。大きい TCP パケットから作成されます。\_\_\_

以前の LSO の要件に加えて、LSOv2 対応ミニポートドライバーも次の条件を満たす必要があります。

-   IPv4 または IPv6 または IPv4 と IPv6 の両方をサポートします。

-   ネットワークインターフェイスカード (NIC) によって生成される各セグメントパケットで、大きなパケットからの IPv4 オプションのレプリケーションをサポートします。

-   各 TCP セグメントパケットで、大きな TCP パケットからの IPv6 拡張ヘッダーのレプリケーションをサポートします。

-   ミニポートドライバーによって生成される各 TCP セグメントパケットにおける TCP オプションのレプリケーションをサポートします。

-   [**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体の IP および tcp ヘッダーをテンプレートとして使用して、各セグメントパケットの tcp/ip ヘッダーを生成します。

-   [IP id (IP ID)] の値は、[0x0000] ~ [の範囲] で使用します。 (0x8000 から0xFFFF までの範囲は TCP chimney オフロード対応デバイス用に予約されています)。たとえば、テンプレートの IP ヘッダーの先頭が Id フィールドの値0x7FFE である場合、最初の TCP セグメントパケットの IP ID 値は0x7FFE で、その後に、0x0001、0x0000、などが続きます。

-   NDIS の**Tcpheaderoffset**メンバーのバイトオフセットを使用して[ **\_tcp\_LARGE\_\_オフロード\_NET\_BUFFER\_LIST\_情報を送信**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_large_send_offload_net_buffer_list_info)して、tcp ヘッダーの場所を特定します。パケットの最初のバイトから開始します。

-   各 LSOv2 [**net\_バッファー\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造に関連付けられている[**NET\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造の数を1に制限します。
    > [!NOTE]
    > これは、LSOv2 対応ミニポートドライバーの新しい要件です。 このルールは、LSOv1 ミニポートドライバーに明示的には適用されませんが、お勧めします。

-   パケットの合計の長さを、NET\_バッファー\_リスト構造内の最初の NET\_バッファー構造の長さから決定します。 これは、 <a href="#lsov1lengthrequirements">LSOv1 で使用</a>される方法とは異なります。

-   TCP オプション、IP オプション、および IP 拡張ヘッダーをサポートします。

-   送信操作が完了すると、ミニポートドライバーは[**NDIS_TCP_LARGE_SEND_OFFLOAD_NET_BUFFER_LIST_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_large_send_offload_net_buffer_list_info)構造体の**LsoV2TransmitComplete**メンバーを0に設定し、 **LsoV2TransmitComplete**メンバーを NDIS_TCP_LARGE_SEND_OFFLOAD_V2_TYPE に設定する必要があります。 