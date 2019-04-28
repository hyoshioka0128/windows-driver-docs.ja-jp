---
title: IPv6 NS オフロードの実装
description: このセクションは、IPv6 近隣要請 (NS) オフロードを実装する方法を説明します
ms.assetid: 48AACE46-4D39-49ED-90AD-F73E27D0CDBE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 685fecb635c435e52ecd5a3f7adde5d6075fbab8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363064"
---
# <a name="implementing-ipv6-ns-offload"></a>IPv6 NS オフロードの実装


NDIS プロトコル ドライバーに送信します (NS) として要求をオフロードする IPv6 近隣要請、 [OID\_PM\_追加\_プロトコル\_オフロード](https://msdn.microsoft.com/library/windows/hardware/ff569763)OID 要求。 これらの NS オフロード要求をサポートするには、ミニポートを次に行う必要があります。

## <a name="indicating-how-many-offload-requests-the-miniport-adapter-supports"></a>ミニポート アダプタのサポートを要求数の負荷を軽減することを示す


ミニポート ドライバーの設定、 **NumNSOffloadIPv6Addresses**のメンバー、 [ **NDIS\_PM\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)を NS の数を示すために構造体オフロード、ミニポート アダプターがサポートを要求します。

**注**  、名前とは異なり、 **NumNSOffloadIPv6Addresses**メンバーには、アドレスの数ではなく、サポートされている要求の数が含まれています。

 

**注**  、一部の Windows ハードウェア認定要件など**Device.Network.LAN.PM.PowMgmtNDIS**と**Device.Network.WLAN.WoWLAN.ImplementWakeOnWLAN**、ミニポート アダプターが少なくとも 2 つの NS オフロード要求をサポートする必要がありますを指定します。 (つまり、他の値、これらの要件に合わせて**NumNSOffloadIPv6Addresses** 2 以上にする必要があります)。詳細については、次を参照してください。、 [Windows 8 ハードウェア認定要件](https://go.microsoft.com/fwlink/p/?linkid=268621)します。

 

各 NS オフロード要求は、1 つまたは 2 のターゲット アドレスを含めることができます。

さらは、NS メッセージの 2 種類があります: ユニキャストとマルチキャストします。 NS メッセージを各ターゲット アドレスの両方の種類に一致するように、ミニポート ドライバーを準備する必要があります。

### <a name="example"></a>例

ミニポート ドライバーが設定されている場合、 [ **NDIS\_PM\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)のメンバー、 **NumNSOffloadIPv6Addresses** NDIS 可能性がありますし、3、構造体送信の最大 3 [OID\_PM\_追加\_プロトコル\_オフロード](https://msdn.microsoft.com/library/windows/hardware/ff569763)種類の要求**NdisPMProtocolOffloadIdIPv6NS**します。 各 OID\_PM\_追加\_プロトコル\_オフロード要求での 1 つまたは 2 つのアドレスがあります、 **TargetIPv6Addresses**のメンバー、 [ **NDIS\_PM\_プロトコル\_オフロード**](https://msdn.microsoft.com/library/windows/hardware/ff566760)構造体。 したがって、ミニポートが 3 x 2 = 6 をサポートする必要がありますターゲット アドレス。

ミニポートがユニキャストの両方に一致する必要があり、各ターゲット アドレス、ミニポートのマルチキャストの NS メッセージは、2 x 6 の合計と一致できる必要がありますので、12 NS メッセージ パターンを = です。

## <a name="matching-the-ns-message"></a>NS メッセージに一致します。


NS メッセージの形式で指定されます[RFC 4861](https://go.microsoft.com/fwlink/p/?linkid=268370) 4.3 の場合、「近隣要請メッセージの形式」のセクションします。 ミニポートは、次の表にフィールドと一致する必要があります。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">フィールド</th>
<th align="left">一致する値</th>
<th align="left">メモ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>Ethernet.EtherType</strong></td>
<td align="left"><p>0x86dd (IPv6)</p></td>
<td align="left"><p>非イーサネット メディアの種類に応じて調整します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>IPv6.Version</strong></td>
<td align="left"><p>6</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>IPv6.NextHeader</strong></td>
<td align="left"><p>58 (ICMPv6)</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>IPv6.HopLimit</strong></td>
<td align="left"><p>255</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>IPv6.Destination</strong></td>
<td align="left"><p><strong>OID。TargetIPv6Addresses [x]</strong>または<strong>OID。SolicitedNodeIPv6Address</strong></p></td>
<td align="left"><p>ミニポートは、このフィールドの両方のオプションと一致する必要があります。<strong>OID。TargetIPv6Addresses [x]</strong>と<strong>OID。SolicitedNodeIPv6Address</strong>します。</p>
<p>このフィールドは場合<strong>OID。TargetIPv6Addresses [x]</strong>、NS メッセージは、ユニキャスト メッセージ。</p>
<p>このフィールドは場合<strong>OID。SolicitedNodeIPv6Address</strong>、NS メッセージがマルチキャストのメッセージ。</p>
<p><strong>OID。TargetIPv6Addresses</strong>は 1 つまたは 2 のアドレスを含むことのできる配列です。 2 つのアドレスがある場合ミニポートに、これらの両方と一致する必要があります。 2 番目のアドレスが「0::0」の場合は、無視する必要があり、2 番目の一致パターンを作成しない必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>IPv6.ICMPv6.Type</strong></td>
<td align="left"><p>135 (NS)</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>IPv6.ICMPv6.Code</strong></td>
<td align="left"><p>0</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>IPv6.ICMPv6.TargetAddress</strong></td>
<td align="left"><p><strong>OID.TargetIPv6Addresses[x]</strong></p></td>
<td align="left"><p><strong>OID。TargetIPv6Addresses [x]</strong>は 1 つまたは 2 のアドレスを含むことのできる配列です。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>IPv6.Source</strong></td>
<td align="left"><p><strong>OID。RemoteIPv6Address</strong></p></td>
<td align="left"><p>場合<strong>OID。RemoteIPv6Address</strong> 「0::0」は、このフィールドを無視する必要があります。</p></td>
</tr>
</tbody>
</table>

 

## <a name="sending-the-na-message"></a>NA メッセージを送信します。


NS メッセージを受信すると、デバイスのファームウェアがで示されて検証手順を実行する必要があります[RFC 4861](https://go.microsoft.com/fwlink/p/?linkid=268370) 7.1 では、「メッセージの検証」、チェックサムの検証などのセクションします。 NS の受信メッセージには、すべての検証が成功した場合はし、NA メッセージを生成され、応答として送信する必要があります。 その形式で指定されます[RFC 4861](https://go.microsoft.com/fwlink/p/?linkid=268370) 4.4、「近隣アドバタイズ メッセージの形式」のセクションします。 ミニポートは、次の表に、フィールドを設定する必要があります。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">フィールド</th>
<th align="left">[値]</th>
<th align="left">メモ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>Ethernet.Destination</strong></td>
<td align="left"><strong>Ethernet.Source</strong></td>
<td align="left"><p>NS フレームからこの値をコピーします。 非イーサネット メディアの種類に応じて調整します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>Ethernet.Source</strong></td>
<td align="left"><p>ミニポートの現在の MAC アドレス</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>IPv6.HopLimit</strong></td>
<td align="left"><p>255</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>IPv6.Source</strong></td>
<td align="left"><strong>IPv6.ICMPv6.TargetAddress</strong></td>
<td align="left"><p>NS フレームからこの値をコピーします。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>IPv6.Destination</strong></td>
<td align="left"><strong>IPv6.Source</strong></td>
<td align="left"><p>しない限り、NS フレームからこの値をコピーの値<strong>IPv6.Source</strong> 「0::0」でした。 場合の値<strong>IPv6.Source</strong> 「0::0」でしたこのフィールドを"FF02::1"に設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>IPv6.ICMPv6.Type</strong></td>
<td align="left"><p>136 (NA)</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>IPv6.ICMPv6.Code</strong></td>
<td align="left"><p>0</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>IPv6.ICMPv6.RouterFlag</strong></td>
<td align="left"><p>0</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>IPv6.ICMPv6.SolicitedFlag</strong></td>
<td align="left"><p>0</p></td>
<td align="left"><p>場合の値<strong>IPv6.Source</strong> ns フレームが「0::0」、このフィールドを 1 に設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>IPv6.ICMPv6.OverrideFlag</strong></td>
<td align="left"><p>1</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>IPv6.ICMPv6.TargetAddress</strong></td>
<td align="left"><strong>IPv6.ICMPv6.TargetAddress</strong></td>
<td align="left"><p>NS フレームからこの値をコピーします。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>IPv6.ICMPv6.TLLAOption.Type</strong></td>
<td align="left"><p>2 (ターゲット リンク層アドレス)</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>IPv6.ICMPv6.TLLAOption.Length</strong></td>
<td align="left"><p>1</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>IPv6.ICMPv6.TLLAOption.LinkLayerAddress</strong></td>
<td align="left"><strong>OID。Mac アドレス</strong></td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

 

 





