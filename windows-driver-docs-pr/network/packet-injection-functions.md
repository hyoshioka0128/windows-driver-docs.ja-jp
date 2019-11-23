---
title: パケット挿入関数
description: パケット挿入関数
ms.assetid: ebbcafb6-7fbf-40e6-8806-0131aa1d4df5
keywords:
- パケット挿入関数 WDK Windows フィルタリングプラットフォーム
- インジェクション関数 WDK Windows フィルタリングプラットフォーム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a49b70f9a63ddcec9d989b8b4fbc995e942d4d39
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843711"
---
# <a name="packet-injection-functions"></a>パケット挿入関数


コールアウトドライバーは、次の WFP 関数を呼び出して、保留または変更されたパケットデータを TCP/IP スタックに挿入できます。 次の表に、データの挿入元として使用できるレイヤーと、可能な変換先を示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">挿入関数</th>
<th align="left">適用可能なレイヤー</th>
<th align="left">宛先</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsinjectforwardasync0" data-raw-source="[&lt;strong&gt;FwpsInjectForwardAsync0&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsinjectforwardasync0)"><strong>FwpsInjectForwardAsync0</strong></a></p></td>
<td align="left"><p>ネットワーク層</p></td>
<td align="left"><p>転送データパス</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsinjectnetworkreceiveasync0" data-raw-source="[&lt;strong&gt;FwpsInjectNetworkReceiveAsync0&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsinjectnetworkreceiveasync0)"><strong>FwpsInjectNetworkReceiveAsync0</strong></a></p></td>
<td align="left"><p>ネットワーク層</p></td>
<td align="left"><p>受信データパス</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsinjectnetworksendasync0" data-raw-source="[&lt;strong&gt;FwpsInjectNetworkSendAsync0&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsinjectnetworksendasync0)"><strong>FwpsInjectNetworkSendAsync0</strong></a></p></td>
<td align="left"><p>ネットワーク層</p></td>
<td align="left"><p>送信データパス</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsinjecttransportreceiveasync0" data-raw-source="[&lt;strong&gt;FwpsInjectTransportReceiveAsync0&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsinjecttransportreceiveasync0)"><strong>FwpsInjectTransportReceiveAsync0</strong></a></p></td>
<td align="left"><p>トランスポート、データグラムデータ、ICMP エラー、または ALE レイヤーからのパケットデータ</p></td>
<td align="left"><p>受信データパス</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsinjecttransportsendasync0" data-raw-source="[&lt;strong&gt;FwpsInjectTransportSendAsync0&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsinjecttransportsendasync0)"><strong>FwpsInjectTransportSendAsync0</strong></a></p></td>
<td align="left"><p>トランスポート、データグラムデータ、ICMP エラー、または ALE レイヤーからのパケットデータ</p></td>
<td align="left"><p>送信データパス</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsstreaminjectasync0" data-raw-source="[&lt;strong&gt;FwpsStreamInjectAsync0&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsstreaminjectasync0)"><strong>FwpsStreamInjectAsync0</strong></a></p></td>
<td align="left"><p>TCP データセグメント</p></td>
<td align="left"><p>データストリーム</p></td>
</tr>
</tbody>
</table>

 

また、 [**FwpsQueryPacketInjectionState0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsquerypacketinjectionstate0)関数を使用して、パケットデータの挿入履歴を検査します。

挿入関数に必要なすべての情報がコールアウトによって提供される場合、クロスレイヤー挿入が有効になります。また、net buffer list は挿入関数によって想定される形式になります。 たとえば、コールアウトは、転送パスでパケットをキャプチャし、その宛先アドレスをローカルコンピューターのアドレスに変更し、 **FwpsInjectTransportReceiveAsync0**を呼び出してパケットをローカルコンピューターの tcp/ip スタックにリダイレクトすることができます。

ストリーム (TCP データ) の挿入を除き、挿入された受信パケットはスタックおよび WFP レイヤーの "最下位" から再入力されますが、挿入された発信パケットはスタックおよび WFP レイヤーの "最上位" から再入力されます。 たとえば、受信データグラムデータレイヤーから挿入された UDP パケットは、スタックを再入力し、ネットワーク層、トランスポート層、ALE 受信または受け入れレイヤー (オプション) をスキャンして、データグラムデータレイヤーに戻します。 送信ネットワークレイヤーから別の UDP パケットが挿入されると、スタックに再入力され、ALE (オプション)、データグラムデータ、およびトランスポート層を走査し、ネットワーク層に戻ります。

**FwpsInjectTransportReceiveAsync0**は、以前は ipsec の検証を通過したため、再挿入パケットの ipsec 処理を自動的にバイパスします。

WFP コールアウトドライバーによって挿入されたパケットは、パケットへの変更によって元のフィルター条件が満たされなくなる場合を除き、コールアウトに再設定されます。 WFP は、コールアウト用の**FwpsQueryPacketInjectionState0**関数を提供して、コールアウトによってパケットが挿入された (または前に挿入された) かどうかを照会します。 無限ループを防ぐために、コールアウトは自己挿入パケットを許可する必要があります。

IP パケットを変更した後、コールアウトは IP またはトランスポート層のチェックサムを調整するか、両方とも調整する必要があります。 コールアウトは、IPv4 パケット上の UDP に対してチェックサムを0に設定できます。 トランスポート層のチェックサムオフロードとの互換性を確保し、それに応じて完全なチェックサムと擬似チェックサムの計算を調整するために、コールアウトは次のロジックを使用できます。

```cpp
NDIS_TCP_IP_CHECKSUM_PACKET_INFO ChecksumInfo;
 ChecksumInfo.Value = 
 (ULONG) (ULONG_PTR)NET_BUFFER_LIST_INFO(
 NetBufferList,TcpIpChecksumNetBufferListInfo);
```

NdisPacketTcpChecksum が**TRUE**の場合、TCP 送信操作はオフロードされます。 ChecksumInfo が**TRUE**の場合は、UDP 送信操作はオフロードされますが、

Windows Vista Service Pack 1 (SP1) および Windows Server 2008 では、Inメタ値-&gt;headerIncludeHeaderLength が0より大きい場合、発信パケットは IP ヘッダーを含む未加工の送信再挿入です。 Windows Vista SP1 および Windows Server 2008 の IP ヘッダーを含む RAW send reinjections を実行するには、複製されたパケットを Inメタ値-&gt;headerIncludeHeaderLength の値で終了し、Inメタ値-&gt;headerIncludeHeader を新しく拡張された領域にコピーする必要があります。 次に、FwpsInjectTransportSendAsync0 をパケットの net buffer リストと共に使用し、FWPS\_TRANSPORT\_SEND\_PARAMS0 パラメーターを**NULL**に設定したままにします。 Net buffer リストの retreat 操作の詳細については、「 [Retreat 操作と](retreat-and-advance-operations.md)詳細な操作」を参照してください。

**注**  未加工の送信操作では、net buffer リストには1つの net バッファーのみを含める必要があります。 Net バッファーの一覧に複数の net バッファーが含まれている場合は、net buffer リストを一連の net buffer リストに変換し、各シリーズの各に1つの net バッファーを含める必要があります。 Net buffer リスト管理の詳細については、「 [net\_のバッファーアーキテクチャ](net-buffer-architecture.md)」を参照してください。

 

 

 





