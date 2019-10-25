---
title: HBA\_バインド\_種類
description: HBA\_バインド\_種類
ms.assetid: a5388574-f48a-4bdc-9ffe-408fa6de1eeb
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c41cf021eecbf8b236150fc9844f954341022425
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838000"
---
# <a name="hba_bind_type"></a>HBA\_バインド\_種類


## <span id="ddk_hba_bind_type_kr"></span><span id="DDK_HBA_BIND_TYPE_KR"></span>


HBA\_BIND\_TYPE WMI class qualifier は、永続的なバインドに関連する特定の機能セットを提供する HBA とそのミニポートドライバーの機能を示します。

次の表に、修飾子名と各名前の意味を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">型</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>HBA_CAN_BIND_TO_D_ID</p></td>
<td align="left"><p>HBA とそのミニポートドライバーが、アドレス識別子によってファイバーチャネルのターゲットポートを識別する永続的なバインドを受け入れることができることを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_CAN_BIND_TO_WWPN</p></td>
<td align="left"><p>HBA とそのミニポートドライバーが、世界中のポート名 (WWPN) によってファイバーチャネルのターゲットポートを識別する永続的なバインドを受け入れることができることを示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_CAN_BIND_TO_WWNN</p></td>
<td align="left"><p>ワールドノード名 (WWNN) によって (ターゲットポートではなく) ファイバーチャネルターゲットデバイスを識別する永続的なバインドを受け入れる、HBA とそのミニポートドライバーの機能を示します。 この方法では、マルチポートデバイスでデバイスを識別するという暗黙のあいまいさは意図的なものです。 これにより、HBA またはファブリックは、ベンダー固有の方法であいまいさを解決することができます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_CAN_BIND_TO_LUID</p></td>
<td align="left"><p>HBA とそのミニポートドライバーが、論理ユニットの SCSI 照会データから派生した識別記述子によってファイバーチャネル論理ユニットを識別する永続的なバインドを受け入れることができるかどうかを示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_CAN_BIND_ANY_LUNS</p></td>
<td align="left"><p>HBA とそのミニポートドライバーが、オペレーティングシステムとファイバーチャネル論理ユニット番号の両方を指定する永続的なバインド設定を受け入れることができるかどうかを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_CAN_BIND_TARGETS</p></td>
<td align="left"><p>HBA とそのミニポートドライバーが、論理ユニットのファイバーチャネルプロトコル (FCP) 識別子と、オペレーティングシステムがバスやターゲットなどの論理ユニットを識別するために使用する情報との間に永続的なバインドを生成する機能を示します。<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_hbascsiid" data-raw-source="[&lt;strong&gt;HBAScsiID&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_hbascsiid)"><strong>HBAScsiID</strong></a>に格納されている数値。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_CAN_BIND_AUTOMAP</p></td>
<td align="left"><p>検出されたすべての記憶域リソースのターゲットマッピングと永続的バインドを自動的に生成するための、HBA とそのミニポートドライバーの機能を示します。 この機能が指定されていない場合、または無効になっている場合、許可されるバインドは、オペレーティングシステムで明示的に構成されているバインディングのみです。 バインドの明示的な構成によって、論理ユニット番号 (LUN) マスクが容易になります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_CAN_BIND_CONFIGURED</p></td>
<td align="left"><p>永続的バインドの動的構成を受け入れるために、HBA とそのミニポートドライバーが使用できるかどうかを示します。</p></td>
</tr>
</tbody>
</table>

 

*Hbaapi. h*を含めることにより、ソフトウェアは、前の表の型名に対応する一連のシンボル定数にアクセスできるようになります。 これらのシンボリック定数の定義は、 *Hbapiwmi* (コンパイル時に WMI ツールスイートによって生成されるファイル) には含まれていません。

 

 





