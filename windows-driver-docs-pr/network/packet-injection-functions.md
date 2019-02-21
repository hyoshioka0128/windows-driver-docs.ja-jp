---
title: パケットの挿入関数
description: パケットの挿入関数
ms.assetid: ebbcafb6-7fbf-40e6-8806-0131aa1d4df5
keywords:
- パケットの挿入関数 WDK Windows フィルタ リング プラットフォーム
- インジェクション関数 WDK Windows フィルタ リング プラットフォーム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e080489c18e8ff80fd1b804e82e5cb0d35d566d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535656"
---
# <a name="packet-injection-functions"></a>パケットの挿入関数


コールアウト ドライバーは保留を挿入する次の WFP 関数を呼び出すことができます。 または TCP/IP スタックにパケット データを変更します。 元のデータを挿入できるか、可能な変換先、と共に適用可能なレイヤーは、次の表に一覧表示されます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">インジェクション関数</th>
<th align="left">該当のレイヤー</th>
<th align="left">宛先</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551177" data-raw-source="[&lt;strong&gt;FwpsInjectForwardAsync0&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551177)"><strong>FwpsInjectForwardAsync0</strong></a></p></td>
<td align="left"><p>ネットワーク層</p></td>
<td align="left"><p>転送データのパス</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551183" data-raw-source="[&lt;strong&gt;FwpsInjectNetworkReceiveAsync0&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551183)"><strong>FwpsInjectNetworkReceiveAsync0</strong></a></p></td>
<td align="left"><p>ネットワーク層</p></td>
<td align="left"><p>受信データのパス</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551185" data-raw-source="[&lt;strong&gt;FwpsInjectNetworkSendAsync0&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551185)"><strong>FwpsInjectNetworkSendAsync0</strong></a></p></td>
<td align="left"><p>ネットワーク層</p></td>
<td align="left"><p>送信データのパス</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551186" data-raw-source="[&lt;strong&gt;FwpsInjectTransportReceiveAsync0&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551186)"><strong>FwpsInjectTransportReceiveAsync0</strong></a></p></td>
<td align="left"><p>トランスポート、データグラム データ、ICMP のエラーまたは ALE レイヤーからのパケット データ</p></td>
<td align="left"><p>受信データのパス</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551188" data-raw-source="[&lt;strong&gt;FwpsInjectTransportSendAsync0&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551188)"><strong>FwpsInjectTransportSendAsync0</strong></a></p></td>
<td align="left"><p>トランスポート、データグラム データ、ICMP のエラーまたは ALE レイヤーからのパケット データ</p></td>
<td align="left"><p>送信データのパス</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551213" data-raw-source="[&lt;strong&gt;FwpsStreamInjectAsync0&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551213)"><strong>FwpsStreamInjectAsync0</strong></a></p></td>
<td align="left"><p>TCP データ セグメント</p></td>
<td align="left"><p>データ ストリーム</p></td>
</tr>
</tbody>
</table>

 

さらに、 [ **FwpsQueryPacketInjectionState0** ](https://msdn.microsoft.com/library/windows/hardware/ff551202)パケット データの挿入の履歴を検査する関数を使用します。

引き出し線の挿入関数で必要とされるすべての必要な情報を指定できる場合クロス レイヤーの挿入が有効になっているし、net バッファーの一覧がインジェクション関数によって予期される形式。 コールアウトが転送パスでパケットをキャプチャ、ローカル コンピューター、および呼び出しの送信先アドレスの変更など**FwpsInjectTransportReceiveAsync0**にパケットをローカル コンピューターの TCP/IP スタックにリダイレクトします。

挿入された受信パケットは、ストリームの (TCP データ) 挿入を除くスタック、WFP レイヤーの"top"から挿入された送信パケットを再入力中にスタック、WFP のレイヤーの"bottom"から再入力します。 たとえば、受信データグラム データ層から挿入 UDP パケットは、スタックを再入力して、ネットワーク層、トランスポート層を走査、ALE が表示されるか (省略可能)、レイヤーをそのまま使用データグラム データ層に戻します。 別の UDP パケット送信のネットワーク層から挿入され、スタックを再入力し ALE (省略可能)、データグラム データ、およびトランスポート層を走査、ネットワーク層にバックアップされます。

**FwpsInjectTransportReceiveAsync0** IPsec IPsec 検証ことになったが以前ので reinjected パケットの処理を自動的にバイパスします。

WFP コールアウト ドライバーによって挿入されたパケットはパケットに変更が元のフィルター条件を見逃すことに原因の場合を除く吹き出しに再指定されます。 WFP が提供、 **FwpsQueryPacketInjectionState0**パケットが挿入された (または前に挿入された) かどうか、クエリへのコールアウトの関数のコールアウトので。 無限ループを防ぐため、コールアウトは、自動挿入されたパケットを許可する必要があります。

コールアウトは、これらの IP パケットを変更後に、IP またはトランスポート層のチェックサム、またはその両方を調整する必要があります。 吹き出しを設定できます、チェックサムを 0 に UDP IPv4 パケットよりも。 トランスポート層のチェックサムとの互換性をオフロードして、吹き出しに擬似チェックサムの計算と完全なチェックサムを適宜調整するには、次のロジックを使用できます。

```cpp
NDIS_TCP_IP_CHECKSUM_PACKET_INFO ChecksumInfo;
 ChecksumInfo.Value = 
 (ULONG) (ULONG_PTR)NET_BUFFER_LIST_INFO(
 NetBufferList,TcpIpChecksumNetBufferListInfo);
```

ChecksumInfo.Transmit.NdisPacketTcpChecksum 場合**TRUE**、TCP 送信の操作がオフロードされます。 ChecksumInfo.Transmit.NdisPacketUdpChecksum 場合**TRUE**UDP の送信操作がオフロードします。

Service Pack 1 (SP1) および Windows Server 2008、Windows Vista で場合 inMetaValues-&gt;headerIncludeHeaderLength が 0 より大きい、パケットの送信は、IP ヘッダーを含む生送信 reinjection します。 Windows Vista SP1 および Windows Server 2008 用の IP ヘッダーを含む生送信 reinjections を実行するのには、inMetaValues-の量で、複製されたパケットを退却&gt;headerIncludeHeaderLength inMetaValues - コピーと&gt;新しく拡張された領域を headerIncludeHeader します。 次に、net バッファーの一覧で、パケットの FwpsInjectTransportSendAsync0 を使用し、FWPS のままに\_トランスポート\_送信\_PARAMS0 パラメーターを設定**NULL**します。 Net のバッファーのリストに撤退操作の詳細については、次を参照してください。[撤退と高度な操作](retreat-and-advance-operations.md)します。

**注**  net バッファーの一覧の生の送信操作では、1 つのネット バッファーのみを含める必要があります。 Net バッファー一覧に 1 つ以上のネットワーク バッファーが含まれている場合、net のバッファーの一覧を一連の net バッファーのリストに変換する必要が、各シリーズの 1 つのネットワーク バッファーを含める必要があります。 Net バッファー リストの管理についての詳細については、次を参照してください。 [NET\_バッファー アーキテクチャ](net-buffer-architecture.md)します。

 

 

 





