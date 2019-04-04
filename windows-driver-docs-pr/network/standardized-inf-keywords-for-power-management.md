---
title: 電源管理用の標準化された INF キーワード
description: 電源管理用の標準化された INF キーワード
ms.assetid: bec8dd96-f64a-40eb-ade9-73c9a66a756e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9e7789589b24256aa2efdff9836b12d3c2df9b4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570730"
---
# <a name="standardized-inf-keywords-for-power-management"></a>電源管理用の標準化された INF キーワード





電源管理の標準化されたキーワードは、デバイス ドライバーの INF ファイルで定義されます。 オペレーティング システムでは、これらの標準的なキーワードを読み込みし、デバイスの現在の電源管理機能を調整します。 デバイス ドライバーは、NDIS 内に、デバイスのハードウェアの電源管理の機能を示す必要があります常に、 [ **NDIS\_ミニポート\_アダプター\_全般\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)構造体。

有効にするか、ネットワーク アダプターの電源管理機能のサポートを無効にするのには、次の標準化された INF キーワードが定義されています。

<a href="" id="-wakeonpattern"></a>**\*WakeOnPattern**  
ネットワーク パケットが、指定したパターンと一致する場合は、コンピューターをスリープ解除するデバイスを有効にするかどうかを示す値。

<a href="" id="-wakeonmagicpacket"></a>**\*WakeOnMagicPacket**  
デバイスが受信すると、コンピューターをウェイクするため、デバイスを有効にするかどうかを示す値を*マジック パケット*します。 (A*マジック パケット*パケットを受信側のネットワーク アダプターのイーサネット アドレスの 16 個の連続したコピーを含む)

<a href="" id="-devicesleepondisconnect"></a>**\*DeviceSleepOnDisconnect**  
低電力状態 (スリープの状態) にデバイスを配置するデバイスを有効にするかどうかを示す値メディアが切断されていると電力の状態 (ウェイク状態) に戻り値のときにメディアが再度に接続します。

<a href="" id="-pmarpoffload"></a>**\*PMARPOffload**  
システムがスリープ状態に入ったときに、アドレス解決プロトコル (ARP) をオフロードするデバイスを有効にするかどうかを示す値。

<a href="" id="-pmnsoffload"></a>**\*PMNSOffload**  
近隣要請 (NS) の負荷を軽減して、システムがスリープ状態に入ったときに、デバイスを有効にするかどうかを示す値。

<a href="" id="-pmwifirekeyoffload"></a>**\*PMWiFiRekeyOffload**  
コンピューターがスリープ状態に入ったとき、一時的なキー (GTK) がウェイク ワイヤレス、LAN (WOL) のキー更新をオフロードするデバイスを有効にするかどうかを示す値をグループ化します。

<a href="" id="-eee"></a>**\*EEE**  
デバイスが IEEE 802.3az を有効にする必要があるかどうかを示す値エネルギー効率の高いイーサネットします。

このトピックの最後にテーブルの列には、列挙型のキーワードは次の属性について説明します。

<a href="" id="subkeyname"></a>SubkeyName  
レジストリ内の INF ファイルに指定する必要があります、キーワードの名前が表示されます。

<a href="" id="paramdesc"></a>ParamDesc  
SubkeyName に関連付けられているテキスト。

<a href="" id="value"></a>値  
リスト内の各オプションに関連付けられている列挙の整数値。 この値は**NDI\\params\\**<em>SubkeyName\\値。</em>

<a href="" id="enumdesc"></a>EnumDesc  
メニューに表示される各値に関連付けられている表示テキスト。

次の表では、電源管理のキーワードの可能な INF エントリについて説明します。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
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
<td align="left"><p>パターン マッチでスリープ解除します。</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 (既定)</p></td>
<td align="left"><p>有効</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>WakeOnMagicPacket</strong></p></td>
<td align="left"><p>Wake on マジック パケット</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 (既定)</p></td>
<td align="left"><p>有効</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>DeviceSleepOnDisconnect</strong></p></td>
<td align="left"><p>デバイスのスリープ状態を切断します。</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 (既定)</p></td>
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
<td align="left"><p>1 (既定)</p></td>
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
<td align="left"><p>1 (既定)</p></td>
<td align="left"><p>有効</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>PMWiFiRekeyOffload</strong></p></td>
<td align="left"><p>WiFi のキーの再発行オフロード</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 (既定)</p></td>
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
<td align="left"><p>1 (既定)</p></td>
<td align="left"><p>有効</p></td>
</tr>
</tbody>
</table>

 

標準化された INF キーワードの詳細については、[ネットワーク デバイスの標準化された INF キーワード](standardized-inf-keywords-for-network-devices.md)を参照してください。

 

 





