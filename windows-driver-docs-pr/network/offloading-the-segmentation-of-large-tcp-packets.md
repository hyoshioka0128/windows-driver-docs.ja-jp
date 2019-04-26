---
title: 大きな TCP パケットのセグメント化のオフロード
description: 大きな TCP パケットのセグメント化のオフロード
ms.assetid: 6ae162fb-a8fc-47b8-80ae-ff39f3059d53
keywords:
- タスクのオフロード WDK TCP/IP トランスポート、大きなパケットのセグメント化
- 大きな TCP パケットのセグメント化 WDK ネットワーク
- 大きな TCP パケットの WDK ネットワー キングのセグメント化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f7a386de570abd90929988ae3fdf142b339e844
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359557"
---
# <a name="offloading-the-segmentation-of-large-tcp-packets"></a>大きな TCP パケットのセグメント化のオフロード





NDIS ミニポート ドライバーでは、ネットワークの中の最大転送単位 (MTU) よりも大きい大きな TCP パケットのセグメント化をオフロードできます。 大きな TCP パケットのセグメント化をサポートする NIC もできない場合があります。

-   IP チェックサム IP オプションを含むパケットの送信を計算します。

-   TCP オプションを含むパケットを送信する TCP チェックサムを計算します。

バージョンの NDIS 6.0 とそれ以降のサポートの大量送信オフロードを多数の送信のような 1 (LSOV1) オフロード、NDIS 5 (LSO) バージョンです。*x*します。 NDIS 6.0 以降のバージョンも多数の送信をサポートしてオフロード バージョン 2 (LSOV2) を提供するには、IPv6 のサポートなど、大きなパケットのセグメント化サービスが強化されています。

LSOV2 と LSOV1 をサポートしているミニポート ドライバーからオフロード型を決定する必要があります、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388) OOB 情報構造体します。 ドライバーを使用して、**型**のメンバー、 [ **NDIS\_TCP\_LARGE\_送信\_オフロード\_NET\_バッファー\_リスト\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff567882) LSOV2 または LSOV1 ドライバー スタックを使用するかどうかを確認して、適切なを実行する構造体サービスの負荷を軽減します。 任意の NET\_バッファー\_LSOv1 または LSOv2 OOB データを含むリスト構造は、1 つも含まれています。 [ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376)構造体。 NDIS の詳細については\_TCP\_LARGE\_送信\_オフロード\_NET\_バッファー\_一覧\_についてを参照してください[TCP/IP へのアクセスNET のオフロード\_バッファー\_情報を一覧表示](accessing-tcp-ip-offload-net-buffer-list-information.md)します。

ただし、ミニポートを受け取った場合に[ **OID\_TCP\_オフロード\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff569807)ミニポート上およびミニポートが LSO 機能を無効にするにはOID が正常に完了、ミニポートはすべて削除されます[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388) 0 ではない LSOv1 または LSOv2 OOB データが含まれている ([ **NDIS\_TCP\_LARGE\_送信\_オフロード\_NET\_バッファー\_一覧\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff567882)). 

TCP/IP トランスポートは、次の条件を満たす大きな TCP パケットのみをオフロードします。

-   パケットは、TCP パケットです。 TCP/IP トランスポートは、セグメント化の大きな UDP パケットをオフロードできません。

-   パケットで割り切れる以上でなければなりません、ミニポート ドライバーで指定されたセグメントの最小数。 詳細については、次を参照してください。[レポート NIC の LSOV1 TCP パケットのセグメンテーション機能](reporting-a-nic-s-lsov1-tcp-packet-segmentation-capabilities.md)と[レポート NIC の LSOV2 TCP パケットのセグメンテーション機能](reporting-a-nic-s-lsov2-tcp-packet-segmentation-capabilities.md)します。

-   パケットはループバック パケットではありません。

-   パケットは、トンネル経由送信されません。

前のセグメント化、TCP/IP トランスポート大きな TCP パケットをオフロードします。

-   関連付けられている大きなパケットのセグメント化情報を更新、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体。 この情報は、 [ **NDIS\_TCP\_LARGE\_送信\_オフロード\_NET\_バッファー\_一覧\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff567882)構造の一部である、 **NET\_バッファー\_一覧**に関連付けられている情報、 **NET\_バッファー\_リスト**構造体。 詳細については**NET\_バッファー\_一覧**についてを参照してください[TCP/IP Offload NET へのアクセス\_バッファー\_情報を一覧表示](accessing-tcp-ip-offload-net-buffer-list-information.md)します。 TCP/IP トランスポートの設定、 **MSS**最大セグメント サイズ (MSS) する値。

-   大きな TCP パケットの合計の長さをパケットの IP ヘッダーの長さの合計フィールドに書き込みます。 長さ合計にはには、IP ヘッダーの長さ、IP のオプションが存在する場合の長さ、TCP ヘッダーの長さ、TCP オプションが、存在する場合の長さ、および TCP ペイロードの長さが含まれています。

-   1 の補数の合計 TCP pseudoheader を計算し、TCP ヘッダーのチェックサム フィールドに、この合計を書き込みます。 TCP/IP トランスポートは、次のフィールド、pseudoheader に対して 1 の補数の合計を計算します。発信元 IP アドレス、宛先 IP アドレス、およびプロトコル。 1 の補数の合計 TCP/IP トランスポートによって提供される pseudoheader は、NIC IP ヘッダーを検査することがなく、NIC が大きな TCP パケットから派生した各パケットの実際の TCP チェックサムの計算に早期の開始を示します。 RFC 793 されて送信元 IP アドレス、宛先 IP アドレス、プロトコル、および長さの TCP 経由で擬似ヘッダーのチェックサムが計算されることに注意してください。 (TCP の長さは、TCP ヘッダーの長さと TCP ペイロードの長さです。 TCP の長さは含まれません擬似ヘッダーの長さ。)ただし、基になるミニポート ドライバーと NIC は、TCP/IP トランスポートによって渡された大規模なパケットから TCP セグメントを生成するため、トランスポート TCP セグメントごとに TCP ペイロードのサイズがわからないし、そのため、TCP の長さ (単位) を含めることはできません。擬似ヘッダー。 代わりに、以下のように、NIC は、生成された各 TCP セグメントの TCP の長さをカバーする TCP/IP トランスポートによって提供された擬似ヘッダーのチェックサムを拡張します。

-   TCP ヘッダーのシーケンス番号のフィールドに適切なシーケンス番号を書き込みます。 シーケンス番号は、TCP ペイロードの最初のバイトを識別します。

後、ミニポート ドライバーを取得、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体の[ *MiniportSendNetBufferLists*](https://msdn.microsoft.com/library/windows/hardware/ff559440)または[ **MiniportCoSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff559365)関数を呼び出すことが、 [ **NET\_バッファー\_]ボックスの一覧\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff568401)マクロが、  *\_Id*の**TcpLargeSendNetBufferListInfo** TCP/IP トランスポートによって書き込まれた MSS 値を取得します。

ミニポート ドライバーでは、パケットの IP ヘッダーから大きなパケットの合計の長さを取得し、MSS 値を使用して、小さなパケットに大きな TCP パケットを分割します。 各小さいパケットには、MSS または少ないユーザー データのバイトが含まれます。 MSS ユーザー データのバイト数より小さいセグメント化された大きなパケットから作成された最後のパケットのみを含める必要がありますに注意してください。 セグメント化されたパケットから作成されたその他のすべてのパケットは、MSS ユーザー データのバイト数を含める必要があります。 このルールを実行しない場合は、作成し、不要な余分なパケットの送信とパフォーマンスが低下でしたします。

ミニポート ドライバーは affixes 大きなパケットから派生した各セグメントに、MAC、IP、および TCP ヘッダーです。 ミニポート ドライバーでは、これらの派生パケットの ip アドレスと TCP チェックサムを計算する必要があります。 (TCP ヘッダーと TCP ペイロード) の TCP チェックサムの可変部分が 1 の補数の合計を計算 pseudoheader にこのチェックサムを追加しますが、NIC を大きな TCP パケットから派生した各パケットに対する TCP チェックサムを計算する計算、TCP/IP トランスポートでは、16 ビットを計算し、チェックサムの 1 の補数。 このようなチェックサムを計算の詳細については、RFC 793 および RFC 1122 を参照してください。

次の図は、大きなパケットのセグメント化を示します。

![大きなパケットのセグメント化を示す図](images/segmentation.png)

大きな TCP パケットで TCP ユーザー データの長さが、ミニポート ドライバーに割り当てられている値以下でする必要があります、 **MaxOffLoadSize**値。 詳細については、 **MaxOffLoadSize**値を参照してください[レポート NIC の LSOV1 TCP パケットのセグメンテーション機能](reporting-a-nic-s-lsov1-tcp-packet-segmentation-capabilities.md)と[NIC の LSOV2 TCP のパケットのセグメンテーションを報告機能](reporting-a-nic-s-lsov2-tcp-packet-segmentation-capabilities.md)します。

ドライバーの問題への変更を示す状態表示した後、 **MaxOffLoadSize**値、ドライバーする必要がありますをクラッシュさせない場合は、以前を使用する LSO 送信要求の受信**MaxOffLoadSize**値。 代わりに、ドライバーには、送信要求が失敗することができます。

変更を報告する状態インジケーターを個別に発行する中間のドライバー、 **MaxOffLoadSize**は状態を示す値を発行していませんが、基になるミニポート アダプターには、すべてのパケットは取得しません値を確認する必要がありますサイズの大きい、 **MaxOffLoadSize**ミニポート アダプターが報告される値。

応答するミニポート中間ドライバー [OID\_TCP\_オフロード\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/ff569807) LSO が要求を送信時間の小さいウィンドウにまだ到達の LSO をオフにするサービスを準備する必要がありますミニポート ドライバー。

セグメントのパケットで TCP ユーザー データの長さは、MSS 以下である必要があります。 MSS は TCP トランスポート LSO NET を使用して渡します ULONG 値\_バッファー\_リストの情報に関連付けられている、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体。 MSS ユーザー データのバイト数より小さいセグメント化された大きなパケットから作成された最後のパケットのみを含める必要がありますに注意してください。 セグメント化されたパケットから作成されたその他のすべてのパケットは、MSS ユーザー データのバイト数を含める必要があります。 このルールを実行しない場合は、作成し、不要な余分なパケットの送信とパフォーマンスが低下でしたします。

以上になる大きな TCP パケットから派生されたセグメントのパケットの数がある必要があります、 **MinSegmentCount**ミニポート ドライバーで指定されている値。 詳細については、 **MinSegmentCount**値を参照してください[レポート NIC の LSOV1 TCP パケットのセグメンテーション機能](reporting-a-nic-s-lsov1-tcp-packet-segmentation-capabilities.md)と[NIC の LSOV2 TCP のパケットのセグメンテーションを報告機能](reporting-a-nic-s-lsov2-tcp-packet-segmentation-capabilities.md)します。

Ip アドレスと TCP ヘッダーの処理には、次の前提条件と制限が適用されます。

-   TCP/IP トランスポート オフロード大きな TCP パケットの IP ヘッダーで MF ビットは設定されませんし、IP ヘッダーには、フラグメントのオフセットはゼロになります。

-   大きな TCP パケットの TCP ヘッダーで URG、RST、および SYN フラグを設定できませんと TCP ヘッダーの緊急のオフセット (ポインター)。 0 になります。

-   大きなパケットの TCP ヘッダーで FIN ビットが設定されている場合、ミニポート ドライバーは、大きな TCP パケットから作成した最後のパケットの TCP ヘッダーでこのビットを設定する必要があります。

-   大きな TCP パケットの TCP ヘッダー内の PSH ビットが設定されている場合、ミニポート ドライバーは、大きな TCP パケットから作成した最後のパケットの TCP ヘッダーでこのビットを設定する必要があります。

-   大きな TCP パケットには、IP オプションまたは TCP オプション (または両方) が含まれています、ミニポート ドライバーは大きな TCP パケットから派生したその各パケットに変更を加えず、これらのオプションをコピーします。 具体的には、NIC にタイムスタンプ オプションは加算されません。

-   すべてのパケット ヘッダー (イーサネット、IP、TCP) は、パケットの最初の MDL になります。 ヘッダーは、複数の MDLs 間で分割されません。 
    > [!TIP]
    > この想定は、LSO を有効にすると有効です。 それ以外の場合、LSO が有効でない場合のミニポート ドライバーとは限りませんイーサネット ヘッダーとして同じ MDL に IP ヘッダーのあります。


ミニポート ドライバーでパケットを送信する必要があります[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)ネットを受信した順序で構造\_バッファー\_一覧TCP/IP トランスポートからの構造体。

大きな TCP パケットを処理するときに、パケットをセグメント化して大きな TCP パケットから派生したパケットの MAC、IP、および TCP ヘッダーを付加することのみをミニポート アダプターが担当します。 TCP/IP トランスポートは、その他のすべてのタスクを実行します (送信を調整するなど、リモート ホストのに基づいてウィンドウ サイズ受信ウィンドウ サイズ)。

大きなパケットの送信操作を完了する前に (などで[ **NdisMSendNetBufferListsComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563668)または[ **NdisMCoSendNetBufferListsComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563570))、ミニポート ドライバーの書き込み、 [ **NDIS\_TCP\_LARGE\_送信\_オフロード\_NET\_バッファー\_リスト\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff567882)値 (NET\_バッファー\_大量送信の一覧情報の負荷を軽減) されたすべてのパケットで正常に送信される TCP ユーザー データのバイト数の合計大きな TCP パケットから作成されます。

前の LSO 要件だけでなく LSOV2 対応のミニポート ドライバー必要があります。

-   IPv4 または IPv6 または IPv4 と IPv6 の両方をサポートします。

-   各セグメント パケット、ネットワーク インターフェイス カード (NIC) を生成する、IPv4 のオプションを大規模なパケットからのレプリケーションをサポートします。

-   各 TCP セグメントのパケットの IPv6 拡張ヘッダーの大きな TCP パケットからのレプリケーションをサポートします。

-   各 TCP セグメント パケット ミニポート ドライバーを生成するには、TCP オプションのレプリケーションをサポートします。

-   Ip アドレスと TCP ヘッダーを使用して、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388) TCP/IP ヘッダー各パケットのセグメントを生成するテンプレートとして構造体。

-   0x0000 ~ 0x7FFF の範囲で IP (IP ID) の id 値を使用します。 (0x8000 ~ 0 xffff の範囲は、TCP chimney オフロード対応デバイス用に予約されて) います。たとえば、テンプレートの IP ヘッダーが、識別フィールドの値の数が 0x7FFE で始まる場合最初 TCP セグメントのパケットは IP ID 値の数が 0x7FFE、0x7FFF、0x0000、0x0001 の後にが必要です。

-   内のバイト オフセットを使用して、 **TcpHeaderOffset**のメンバー [ **NDIS\_TCP\_LARGE\_送信\_オフロード\_NET\_バッファー\_一覧\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff567882)パケットの最初のバイトから、TCP ヘッダーの場所を特定します。

-   数を制限[ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376)構造に関連付けられた各 LSOV2 [ **NET\_バッファー\_]ボックスの一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体。

-   最初の NET の長さからのパケットの合計の長さを決定\_ネット バッファー構造\_バッファー\_リスト構造体。

-   TCP、IP、および拡張機能の IP ヘッダーをサポートします。

-   送信操作が完了したら、ミニポート ドライバーを設定する必要があります、 **LsoV2TransmitComplete.Reserved**のメンバー、 [ **NDIS_TCP_LARGE_SEND_OFFLOAD_NET_BUFFER_LIST_INFO** ](https://msdn.microsoft.com/library/windows/hardware/ff567882)をゼロに構造体と**LsoV2TransmitComplete.Type** NDIS_TCP_LARGE_SEND_OFFLOAD_V2_TYPE するメンバー。 
 

 





