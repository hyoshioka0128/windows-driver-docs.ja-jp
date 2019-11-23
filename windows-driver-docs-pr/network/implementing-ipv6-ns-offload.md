---
title: IPv6 NS オフロードの実装
description: このセクションでは、IPv6 近隣要請 (NS) オフロードを実装する方法について説明します。
ms.assetid: 48AACE46-4D39-49ED-90AD-F73E27D0CDBE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d31487cbad6874e54437ed5070d8fe103c66d488
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843637"
---
# <a name="implementing-ipv6-ns-offload"></a>IPv6 NS オフロードの実装


NDIS プロトコルドライバーは、IPv6 近隣要請 (NS) オフロード要求を OID\_PM として送信し[\_\_プロトコル\_オフロード](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-add-protocol-offload)OID 要求を追加します。 これらの NS オフロード要求をサポートするために、ミニポートは次の操作を実行します。

## <a name="indicating-how-many-offload-requests-the-miniport-adapter-supports"></a>ミニポートアダプターがサポートするオフロード要求の数を示します。


ミニポートドライバーは、ミニポートアダプターがサポートする NS オフロード要求の数を示すために、 [**NDIS\_PM\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)構造の**NumNSOffloadIPv6Addresses**メンバーを設定します。

**  名前**にかかわらず、 **NumNSOffloadIPv6Addresses**メンバーには、アドレス数ではなく、サポートされている要求の数が含まれています。

 

**注  :** **PowMgmtNDIS**や**ImplementWakeOnWLAN**など、一部の Windows ハードウェア認定要件は、ミニポートアダプターが少なくとも2つの NS オフロード要求をサポートする必要があることを指定します。 (つまり、これらの要件を満たすには、 **NumNSOffloadIPv6Addresses**の値が2以上である必要があります)。詳細については、「 [Windows 8 のハードウェア認定の要件](https://go.microsoft.com/fwlink/p/?linkid=268621)」を参照してください。

 

各 NS オフロード要求には、1つまたは2つのターゲットアドレスを含めることができます。

また、NS メッセージには、ユニキャストとマルチキャストの2種類があります。 ミニポートドライバーは、各ターゲットアドレスの両方の種類の NS メッセージに一致するように準備する必要があります。

### <a name="example"></a>例

ミニポートドライバーによって、 **NumNSOffloadIPv6Addresses**構造体の[**ndis\_pm\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)メンバーが3に設定されている場合、ndis は**NdisPMProtocolOffloadIdIPv6NS**型の[\_プロトコル\_オフロード要求を追加\_最大 3 OID\_pm](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-add-protocol-offload)を送信することがあります。 各 OID\_PM\_追加\_プロトコル\_オフロード要求には、 [**NDIS\_PM\_プロトコル\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)構造の**TargetIPv6Addresses**メンバー内のアドレスが1つまたは2つだけ含まれる場合があります。 そのため、ミニポートでは、3 x 2 = 6 個のターゲットアドレスがサポートされている必要があります。

ミニポートは、各ターゲットアドレスのユニキャストとマルチキャストの両方の NS メッセージに一致する必要があるため、ミニポートは、合計 6 x 2 = 12 の NS メッセージパターンと一致している必要があります。

## <a name="matching-the-ns-message"></a>NS メッセージの照合


NS メッセージ形式は、 [RFC 4861](https://go.microsoft.com/fwlink/p/?linkid=268370)セクション4.3 の "近隣要請メッセージ形式" で指定されています。 ミニポートは、次の表のフィールドと一致している必要があります。

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
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>EtherType</strong></td>
<td align="left"><p>0x86dd (IPv6)</p></td>
<td align="left"><p>必要に応じて、非イーサネットメディアの種類に合わせて調整します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>IPv6. バージョン</strong></td>
<td align="left"><p>6</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>NextHeader</strong></td>
<td align="left"><p>58 (ICMPv6)</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>HopLimit</strong></td>
<td align="left"><p>255</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>IPv6. 宛先</strong></td>
<td align="left"><p><strong>OID。TargetIPv6Addresses [x]</strong>または<strong>OID。SolicitedNodeIPv6Address</strong></p></td>
<td align="left"><p>ミニポートは、このフィールドの両方のオプション (OID) に一致する必要があります<strong>。TargetIPv6Addresses [x]</strong>と<strong>OID。SolicitedNodeIPv6Address</strong>。</p>
<p>このフィールドが OID の場合は<strong>。TargetIPv6Addresses [x]</strong>、NS メッセージはユニキャストメッセージです。</p>
<p>このフィールドが OID の場合は<strong>。SolicitedNodeIPv6Address</strong>、NS メッセージはマルチキャストメッセージです。</p>
<p><strong>OID。TargetIPv6Addresses</strong>は、1つまたは2つのアドレスを含むことができる配列です。 2つのアドレスが含まれている場合、ミニポートは両方のアドレスに一致する必要があります。 2番目のアドレスが "0::0" の場合は無視する必要があり、2番目の一致パターンを作成することはできません。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>「IPv6. ICMPv6.」と入力します。</strong></td>
<td align="left"><p>135 (NS)</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>IPv6. ICMPv6. コード</strong></td>
<td align="left"><p>0</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>TargetAddress</strong></td>
<td align="left"><p><strong>ドーナツ.TargetIPv6Addresses [x]</strong></p></td>
<td align="left"><p><strong>OID。TargetIPv6Addresses [x]</strong>は、1つまたは2つのアドレスを含むことができる配列です。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>IPv6. ソース</strong></td>
<td align="left"><p><strong>ドーナツ.RemoteIPv6Address</strong></p></td>
<td align="left"><p><strong>OID の場合は。RemoteIPv6Address</strong>は "0::0" です。このフィールドは無視してください。</p></td>
</tr>
</tbody>
</table>

 

## <a name="sending-the-na-message"></a>NA メッセージの送信


デバイスのファームウェアは、NS メッセージを受信すると、 [RFC 4861](https://go.microsoft.com/fwlink/p/?linkid=268370)セクション7.1 の「メッセージの検証」に記載されている検証手順を実行します。チェックサムの検証も含まれます。 受信 NS メッセージがすべての検証に合格した場合は、NA メッセージを生成し、応答として送信する必要があります。 この形式は、 [RFC 4861](https://go.microsoft.com/fwlink/p/?linkid=268370)のセクション4.4 の "近隣通知メッセージの形式" で指定されています。 ミニポートでは、次の表に示すフィールドを設定する必要があります。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">フィールド</th>
<th align="left">Value</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>イーサネット. 宛先</strong></td>
<td align="left"><strong>イーサネット。ソース</strong></td>
<td align="left"><p>この値は、NS フレームからコピーします。 必要に応じて、非イーサネットメディアの種類に合わせて調整します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>イーサネット。ソース</strong></td>
<td align="left"><p>ミニポートの現在の MAC アドレス</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>HopLimit</strong></td>
<td align="left"><p>255</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>IPv6. ソース</strong></td>
<td align="left"><strong>TargetAddress</strong></td>
<td align="left"><p>この値は、NS フレームからコピーします。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>IPv6. 宛先</strong></td>
<td align="left"><strong>IPv6. ソース</strong></td>
<td align="left"><p><strong>IPv6</strong>の値が "0::0" でない場合は、この値を NS フレームからコピーします。 <strong>IPv6</strong>の値が "0::0" の場合このフィールドを "FF02:: 1" に設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>「IPv6. ICMPv6.」と入力します。</strong></td>
<td align="left"><p>136 (NA)</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>IPv6. ICMPv6. コード</strong></td>
<td align="left"><p>0</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>IPv6. ルーターフラグ</strong></td>
<td align="left"><p>0</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>SolicitedFlag</strong></td>
<td align="left"><p>0</p></td>
<td align="left"><p>NS フレームの<strong>IPv6</strong>の値が "0::0" の場合は、このフィールドを1に設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>OverrideFlag</strong></td>
<td align="left"><p>1</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>TargetAddress</strong></td>
<td align="left"><strong>TargetAddress</strong></td>
<td align="left"><p>この値は、NS フレームからコピーします。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>IPv6... TLLAOption. 型</strong></td>
<td align="left"><p>2 (ターゲットリンク層アドレス)</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>IPv6. ICMPv6. TLLAOption. Length</strong></td>
<td align="left"><p>1</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>[IPv6.... Linkレイヤーアドレス]</strong></td>
<td align="left"><strong>ドーナツ.Mac</strong></td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

 

 





