---
title: 電源管理用の標準化された INF キーワード
description: 電源管理用の標準化された INF キーワード
ms.assetid: bec8dd96-f64a-40eb-ade9-73c9a66a756e
ms.date: 08/01/2019
ms.localizationpriority: medium
ms.openlocfilehash: ec32cac72955b92fecc9db9cd96c5306a4826e4c
ms.sourcegitcommit: e2e4746c0efe082296c18de7ab14a1901e2eda9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71716938"
---
# <a name="standardized-inf-keywords-for-power-management"></a>電源管理用の標準化された INF キーワード

電源管理の標準化されたキーワードは、デバイスドライバーの INF ファイルで定義されています。 オペレーティングシステムは、これらの標準化されたキーワードを読み取って、デバイスの現在の電源管理機能を調整します。 デバイスドライバーは、ndis [ **\_ミニポート\_\_アダプターの\_一般属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)構造で、ndis に対するデバイスのハードウェア電源管理機能を常に示す必要があります。

次の標準化された INF キーワードは、ネットワークアダプターの電源管理機能のサポートを有効または無効にするために定義されています。

<a href="" id="-wakeonpattern"></a> **\*WakeOnPattern**  
ネットワークパケットが指定したパターンに一致した場合に、コンピューターのスリープを解除するようにデバイスを有効にするかどうかを示す値。

<a href="" id="-wakeonmagicpacket"></a> **\*WakeOnMagicPacket**  
デバイスが*マジックパケット*を受信したときにコンピューターをスリープ解除するようにデバイスを有効にするかどうかを示す値。 (*マジックパケット*とは、受信側のネットワークアダプターのイーサネットアドレスの連続した16個のコピーを含むパケットです)。

<a href="" id="-modernstandbywolmagicpacket"></a> **\*ModernStandbyWoLMagicPacket**  
デバイスが*マジックパケット*を受信し、システムが*S0ix*の電源状態であるときに、コンピューターのスリープを解除するためにデバイスを有効にする必要があるかどうかを示す値。 システムが*S4*の電源状態にある場合は、この設定は適用されません。

> [!NOTE]
> **\*ModernStandbyWoLMagicPacket**は、NDIS 6.60 以降、または Windows 10 バージョン1607以降でサポートされています。

<a href="" id="-devicesleepondisconnect"></a> **\*DeviceSleepOnDisconnect**  
メディアが切断されたときにデバイスを低電力状態 (スリープ状態) にするようにデバイスを有効にするかどうかを示す値。メディアが再び接続されている場合は、デバイスを電力の状態 (ウェイク状態) に戻す必要があります。

<a href="" id="-pmarpoffload"></a> **\*PMARPOffload**  
システムがスリープ状態になったときに、アドレス解決プロトコル (ARP) のオフロードをデバイスで有効にする必要があるかどうかを示す値。

<a href="" id="-pmnsoffload"></a> **\*PMNSOffload**  
システムがスリープ状態になったときに近隣要請 (NS) をオフロードするようにデバイスを有効にする必要があるかどうかを示す値。

<a href="" id="-pmwifirekeyoffload"></a> **\*Pmwi焼討 Keyoffload**  
コンピューターがスリープ状態になったときに wake on ワイヤレス LAN (WOL) のグループテンポラル (GTK) のキー更新をオフロードするようにデバイスを有効にする必要があるかどうかを示す値。

<a href="" id="-eee"></a> **\*ぃ**  
デバイスで IEEE 802.3 az エネルギー効率の高いイーサネットを有効にする必要があるかどうかを示す値。

このトピックの最後にある表の列では、列挙型キーワードの次の属性について説明します。

<a href="" id="subkeyname"></a>SubkeyName  
INF ファイルで指定する必要があり、レジストリに表示されるキーワードの名前。

<a href="" id="paramdesc"></a>ParamDesc  
SubkeyName に関連付けられている表示テキスト。

<a href="" id="value"></a>数値  
リスト内の各オプションに関連付けられている列挙整数値。 この値は、 **ndi\\params\\** <em>subkeyname\\値</em>に格納されます。

<a href="" id="enumdesc"></a>EnumDesc  
メニューに表示される各値に関連付けられている表示テキスト。

次の表は、電源管理のキーワードに使用できる INF エントリを示しています。

<table>  
<colgroup><col width="25%" /> <col width="25%" /> <col width="25%" /> <col width="25%" /></colgroup>  
<thead>  
<tr class="header">  
<th align="left">SubkeyName</th>
<th align="left">ParamDesc</th>
<th align="left">[値]</th>
<th align="left">EnumDesc</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em>WakeOnPattern</strong></p></td>
<td align="left"><p>Wake on パターン一致</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 (既定値)</p></td>
<td align="left"><p>有効</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>WakeOnMagicPacket</strong></p></td>
<td align="left"><p>マジックパケットの Wake on</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 (既定値)</p></td>
<td align="left"><p>有効</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>ModernStandbyWoLMagicPacket</strong></p></td>
<td align="left"><p>システムが<i>S0ix</i>の電源状態にあるときのマジックパケットの Wake on</p></td>
<td align="left"><p>0 (既定値)</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>有効</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>DeviceSleepOnDisconnect</strong></p></td>
<td align="left"><p>切断時にデバイスをスリープ状態にする</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 (既定値)</p></td>
<td align="left"><p>有効</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>PMARPOffload</strong></p></td>
<td align="left"><p>ARP オフロード</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 (既定値)</p></td>
<td align="left"><p>有効</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>PMNSOffload</strong></p></td>
<td align="left"><p>NS オフロード</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 (既定値)</p></td>
<td align="left"><p>有効</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>PMWiFiRekeyOffload</strong></p></td>
<td align="left"><p>WiFi のキー更新のオフロード</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 (既定値)</p></td>
<td align="left"><p>有効</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>* EEE</strong></p></td>
<td align="left"><p>エネルギー効率の高いイーサネット</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 (既定値)</p></td>
<td align="left"><p>有効</p></td>
</tr>
</tbody>
</table>

 

標準化された INF キーワードの詳細については、「[ネットワークデバイスの標準化](standardized-inf-keywords-for-network-devices.md)された inf キーワード」を参照してください。

 

 





