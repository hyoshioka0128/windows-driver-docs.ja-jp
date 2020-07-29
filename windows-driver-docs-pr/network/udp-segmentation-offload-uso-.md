---
title: UDP セグメント化オフロード (USO)
description: UDP セグメント化オフロード (USO)
ms.assetid: 7B9E42DD-0DAD-478A-BF6B-B83A0A236E36
keywords:
- ネットワークドライバー WDK、UDP セグメント化オフロード (USO)
- UDP セグメント化オフロード (USO) の WDK ネットワーク
- UDP セグメント化オフロード (USO) の WDK ネットワーク、UDP セグメント化オフロード (USO)
- UDP セグメント化オフロード (USO) について
ms.date: 02/27/2020
ms.localizationpriority: medium
ms.openlocfilehash: 8604cc8bc68758ec2efc66d411782720d988619c
ms.sourcegitcommit: 9102e34c3322d8697dbb6f9a1d78879147a73373
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/28/2020
ms.locfileid: "87294990"
---
# <a name="udp-segmentation-offload-uso"></a>UDP セグメント化オフロード (USO)

Windows 10 バージョン1912以降でサポートされる UDP セグメンテーションオフロード (USO) は、ネットワークインターフェイスカード (Nic) がネットワークメディアの最大転送単位 (MTU) を超える UDP データグラムのセグメント化をオフロードできる機能です。 これにより、Windows はパケットごとの TCP/IP 処理に関連する CPU 使用率を削減します。 USO の要件は、TCP トランスポートプロトコル用の[LSOv2](offloading-the-segmentation-of-large-tcp-packets.md)に似ています。

## <a name="requirements-for-uso"></a>USO の要件

このセクションでは、主に NDIS プロトコルとミニポートドライバーについて説明します。 NDIS ライトウェイトフィルタードライバー (LWFs) は、パケットを変更または送信するときにプロトコルドライバーの要件に従う必要があります。また、 [*Filtersendnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_send_net_buffer_lists)ハンドラーに提供されるパケットがプロトコルドライバーの要件を満たしていると想定することもできます。

ミニポートドライバーを使用すると、ネットワークメディアの MTU より大きい大きな UDP パケットのセグメント化をオフロードできます。 大きな UDP パケットのセグメント化をサポートする NIC では、次の操作も実行できる必要があります。

- IPv4 オプションを含む送信パケットの IP チェックサムを計算する
- 送信パケットの UDP チェックサムを計算する

USO をサポートするミニポートドライバーでは、 [**NET_BUFFER_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造の帯域外 (OOB) 情報からオフロードの種類を決定する必要があります。 [**NDIS_UDP_SEGMENTATION_OFFLOAD_NET_BUFFER_LIST_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_udp_segmentation_offload_net_buffer_list_info)構造体の値が0以外の場合、ミニポートドライバーは uso を実行する必要があります。 USO OOB データを含むすべての**NET_BUFFER_LIST**にも、1つの[**NET_BUFFER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)構造が含まれています。 ただし、ミニポートドライバーで USO を無効にする[OID_TCP_OFFLOAD_PARAMETERS](oid-tcp-offload-parameters.md)を受信した場合は、ミニポートドライバーが OID を正常に完了した後で、USO OOB フィールドが設定されている**NET_BUFFER_LIST**を拒否して返す必要があります。

TCP/IP トランスポートは、次の条件を満たす UDP パケットだけをオフロードします。

- パケットは UDP パケットです。
- パケット長は、最大セグメントサイズ **(MSS) \* (MinSegmentCount-1)** よりも大きくする必要があります。
- ミニポートドライバーで**SubMssFinalSegmentSupported**機能が設定されていない場合、トランスポートによってオフロードされる各大きな UDP パケットの**長さは% MSS = = 0**である必要があります。 つまり、サイズの大きいパケットは、厳密に**MSS**ユーザーバイトを含むパケットセグメントごとに**N 個**のパケットに割り切れます。 ミニポートドライバーによって**SubMssFinalSegmentSupported**機能が設定されている場合、トランスポートのこのパケット長 divisibility 条件は適用されません。 つまり、最後のセグメントは、 **MSS**よりも小さくなる可能性があります。
- パケットがループバックパケットではありません。
- TCP/IP トランスポートオフロードを行う大きな UDP パケットの IP ヘッダーの**MF**ビットは設定されず、ip ヘッダー内の**フラグメントオフセット**はゼロになります。
- アプリケーションで UDP_SEND_MSG_SIZE/[Wsasetudpsendmessagesize](https://docs.microsoft.com/windows/win32/api/ws2tcpip/nf-ws2tcpip-wsasetudpsendmessagesize)が指定されました。

大量の UDP パケットのセグメント化をオフロードする前に、TCP/IP トランスポートは次のことを行います。

- [**NET_BUFFER_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造に関連付けられている大量のパケットセグメンテーション情報を更新します。 この情報は、 **NET_BUFFER_LIST**構造の OOB 情報の一部である[**NDIS_UDP_SEGMENTATION_OFFLOAD_NET_BUFFER_LIST_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_udp_segmentation_offload_net_buffer_list_info)構造です。 TCP/IP トランスポートは、MSS 値を目的の MSS に設定します。
- UDP 擬似ヘッダーの1の補数の合計を計算し、この合計を UDP ヘッダーの**チェックサム**フィールドに書き込みます。 TCP/IP トランスポートは、擬似ヘッダー内の次のフィールドについて、発信元 IP アドレス、宛先 IP アドレス、およびプロトコルについて、1が補完する値を計算します。  

TCP/IP トランスポートによって提供される疑似ヘッダーの補数合計は、nic が大きな UDP パケットから派生した各パケットの実際の UDP チェックサムの計算を開始するときに、IP ヘッダーを調べる必要はありません。 

[Rfc 768](https://tools.ietf.org/html/rfc768)および[rfc 2460](https://tools.ietf.org/html/rfc2460)では、発信元 IP アドレス、宛先 ip アドレス、プロトコル、および UDP の長さ (udp ヘッダーの長さと udp ペイロードの長さを加算したものではなく、擬似ヘッダーの長さを除く) に対して擬似ヘッダーが計算されることが規定されていることに注意してください。 ただし、基になるミニポートドライバーと NIC は、TCP/IP トランスポートによって渡される大きなパケットから UDP データグラムを生成するため、各 UDP データグラムの UDP ペイロードのサイズを認識しないため、擬似ヘッダーの計算に UDP の長さを含めることはできません。 代わりに、次のセクションで説明するように、NIC は、生成された各 UDP データグラムの UDP の長さに対応するために、TCP/IP トランスポートによって提供された擬似ヘッダーチェックサムを拡張します。

> [!IMPORTANT]
> TCP/IP トランスポートによって提供される UDP ヘッダーチェックサムフィールドがゼロの場合、NIC は UDP チェックサム計算を実行しません。

## <a name="sending-packets-with-uso"></a>USO を使用したパケットの送信

ミニポートドライバーは、 [*Miniportsendnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)コールバック関数内の[**NET_BUFFER_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)を取得した後、 **UdpSegmentationOffloadInfo**の **_Id**を使用して[**NET_BUFFER_LIST_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-net_buffer_list_info)マクロを呼び出して、MSS 値と IP プロトコルを取得できます。

ミニポートドライバーは、最初の[**NET_BUFFER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)構造の長さから大きなパケットの合計長を取得し、 **MSS**値を使用して大きな UDP パケットを小さい udp パケットに分割します。 小さいパケットには、 **MSS**以下のユーザーデータバイトが含まれます。 セグメント化された大きいパケットから作成された最後のパケットのみが、 **MSS**ユーザーデータバイト未満であることに注意してください。 セグメント化されたパケットから作成された他のすべてのパケットには、 **MSS**ユーザーデータバイトが含まれている必要があります。 ミニポートドライバーがこの規則に準拠していない場合、UDP データグラムは誤って配信されます。 ミニポートドライバーによって**SubMssFinalSegmentSupported**機能が設定されていない場合、パケット長は**mss**によって分割され、セグメント化された各パケットには**mss**ユーザーバイトが含まれます。

ミニポートドライバーは、大きなパケットから派生した各セグメントに対して、MAC、IP、および UDP ヘッダーを接辞します。 ミニポートドライバーは、これらの派生パケットの IP チェックサムと UDP チェックサムを計算する必要があります。 大きな UDP パケットから派生した各パケットの UDP チェックサムを計算するために、NIC は udp チェックサムの可変部分 (UDP ヘッダーおよび UDP ペイロード用) を計算し、このチェックサムを TCP/IP トランスポートによって計算された擬似ヘッダーの1の補数の合計に追加して、チェックサムの16ビット1の補数を計算します。 このようなチェックサムの計算の詳細については、 [rfc 768](https://tools.ietf.org/html/rfc768)および[rfc 2460](https://tools.ietf.org/html/rfc2460)を参照してください。 

大きな UDP パケット内の UDP ユーザーデータの長さは、ミニポートドライバーが**Maxoffloadsize**値に割り当てる値以下である必要があります。

ドライバーは、 **Maxoffloadsize**値が変更されたことを示すステータスを発行した後、前の**maxoffloadsize**値を使用する LSO 送信要求を受け取った場合に、バグチェックを行わないようにする必要があります。 代わりに、ドライバーは送信要求を失敗させる必要があります。 ドライバーは、実行できない送信要求を何らかの理由 (サイズ、最小セグメント数、IP オプションなど) に対して失敗させる**必要があり**ます。 ドライバーは、機能が変更された場合に、できるだけ早くステータスを送信する必要があります。

**Maxoffloadsize**値が変更されたことを報告するステータス表示を個別に発行する中間ドライバーは、ステータスが示されていない基になるミニポートアダプターが、ミニポートアダプターが報告した**maxoffloadsize**値より大きいパケットを取得しないようにする必要があります。

USO サービスの電源をオフにする[OID_TCP_OFFLOAD_PARAMETERS](oid-tcp-offload-parameters.md)に応答するミニポート中間ドライバーは、uso 要求がミニポートドライバーに到着する可能性がある小さな時間帯に備えて準備する必要があります。

大きな UDP パケットから派生されたセグメント化パケットの数は、ミニポートドライバーによって指定された**MinSegmentCount**の値以上である必要があります。

大きな UDP パケットを処理する場合、ミニポートドライバーは、パケットと付加の MAC、IP、および UDP ヘッダーを大きな UDP パケットから派生したパケットに分割するだけで済みます。 ミニポートが1つ以上のセグメント化されたパケットの送信に失敗した場合、NBL は、最終的にはエラー状態で完了する必要があります。 ミニポートは後続のパケットの送信を続行できますが、そのためには必要ありません。 すべてのセグメント化されたパケットが送信または失敗するまで、NBL を NDIS に戻すことはできません。

USO 対応のミニポートドライバーでは、次の操作も行う必要があります。

- IPv4 と IPv6 の両方をサポートします。
- NIC によって生成されるセグメント化された各パケットの大きなパケットからの IPv4 オプションのレプリケーションをサポートします。
- [**NET_BUFFER_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造の IP および udp ヘッダーをテンプレートとして使用して、セグメント化された各パケットの UDP ヘッダーと IP ヘッダーを生成します。
- [IP id (IP ID)] の値は、[ **0x0000** ] ~ [ **0xffff**] の範囲内で使用します。 たとえば、テンプレートの IP ヘッダーの先頭が Id フィールドの値が**0xFFFE**の場合、最初の UDP データグラムのパケットの値は**0xFFFE**で、その後に**0xffff**、 **0x0000**、 **0x0001**などを指定する必要があります。
- 大きい UDP パケットに IP オプションが含まれている場合、ミニポートドライバーは、これらのオプションを変更せずに、大きな UDP パケットから派生した各パケットにコピーします。
- [**NDIS_UDP_SEGMENTATION_OFFLOAD_NET_BUFFER_LIST_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_udp_segmentation_offload_net_buffer_list_info)の**UdpHeaderOffset**メンバーのバイトオフセットを使用して、パケットの最初のバイトから開始する UDP ヘッダーの場所を決定します。
- セグメント化されたパケットに基づいて、送信統計をインクリメントします。 たとえば、各パケットセグメントのイーサネット、IP、および UDP ヘッダーのバイト数を含め、パケット数は**1**ではなく、 **MSS**サイズのセグメントの数を示します。
- セグメント化されたデータグラムのサイズごとに、UDP の合計長と IP の長さのフィールドを設定します。

## <a name="ndis-interface-changes"></a>NDIS インターフェイスの変更

このセクションでは、ホストの TCP/IP ドライバースタックがミニポートドライバーによって公開される USO 機能を利用できるようにする NDIS 6.83 の変更について説明します。

NDIS とミニポートドライバーは、次の処理を実行します。

- NIC が USO 機能をサポートしていることを提供する
- USO を有効または無効にする
- 現在の USO 機能の状態を取得します。

### <a name="advertising-uso-capability"></a>USO 機能のアドバタイズ

ミニポートドライバーは、UdpSegmentation 構造体[**NDIS_OFFLOAD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload)の**UdpSegmentation**フィールドに入力することで、uso 機能を提供します。これは、 [**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)のパラメーターに渡されます。 **NDIS_OFFLOAD**構造体の**header. Revision**フィールドは**NDIS_OFFLOAD_REVISION_6**に設定する必要があります。また、 **Size**フィールドは**NDIS_SIZEOF_NDIS_OFFLOAD_REVISION_6**に設定する必要があります。

### <a name="querying-uso-state"></a>USO 状態のクエリ

現在の USO の状態は、 [OID_TCP_OFFLOAD_CURRENT_CONFIG](oid-tcp-offload-current-config.md)で照会できます。 この OID は NDIS によって処理され、ミニポートドライバーには渡されません。

### <a name="changing-uso-state"></a>USO 状態の変更

USO は[OID_TCP_OFFLOAD_PARAMETERS](oid-tcp-offload-parameters.md)を使用して有効または無効にすることができます。 ミニポートドライバーは OID を処理した後、更新されたオフロード状態を含む[NDIS_STATUS_TASK_OFFLOAD_CURRENT_CONFIG](ndis-status-task-offload-current-config.md)状態の通知を送信する必要があります。

## <a name="uso-keywords"></a>USO キーワード

USO 列挙型のキーワードは次のとおりです。

- **\*UsoIPv4**
- **\*UsoIPv6**

これらの値は、その特定の IP プロトコルで USO が有効になっているか無効になっているかを示します。 USO の設定は、 [**NDIS_TCP_IP_CHECKSUM_OFFLOAD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload)の構成に依存しません。 たとえば、 ** \* UDPChecksumOffloadIPv4**を無効にしても、 ** \* UsoIPv4**は暗黙的に無効になりません。

| サブキーの名前 | パラメーターの説明 | 値 | 列挙型の説明 |
| --- | --- | --- | --- |
| **\*UsoIPv4** | UDP セグメント化オフロード (IPv4) | 0 | 無効 |
|   |   | 1 | Enabled |
| **\*UsoIPv6** | UDP セグメント化オフロード (IPV6) | 0 | 無効 |
|   |   | 1 | Enabled |