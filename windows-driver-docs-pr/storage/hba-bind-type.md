---
title: HBA\_バインド\_型
description: HBA\_バインド\_型
ms.assetid: a5388574-f48a-4bdc-9ffe-408fa6de1eeb
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 682959a9a7c1832667884ede58694b3611528741
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383105"
---
# <a name="hbabindtype"></a>HBA\_バインド\_型


## <span id="ddk_hba_bind_type_kr"></span><span id="DDK_HBA_BIND_TYPE_KR"></span>


HBA\_バインド\_型 WMI クラスの修飾子は、永続的なバインディングに関連する機能の特定のセットを提供するには、HBA の機能とそのミニポート ドライバーを示します。

次の表は、修飾子の名前と各名前の意味を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">型</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>HBA_CAN_BIND_TO_D_ID</p></td>
<td align="left"><p>HBA の機能、およびそのアドレスの識別子を使用して、ファイバー チャネルのターゲット ポートを識別する永続的なバインドを受け入れるように、ミニポート ドライバーを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_CAN_BIND_TO_WWPN</p></td>
<td align="left"><p>HBA の機能と、世界中のポート名 (WWPN) で、ファイバー チャネルのターゲット ポートを識別する永続的なバインドを受け入れるように、ミニポート ドライバーを示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_CAN_BIND_TO_WWNN</p></td>
<td align="left"><p>HBA の機能と、世界中のノード名 (WWNN) でファイバー チャネルのターゲット デバイス (ターゲット ポートではなく) を識別する永続的なバインドを受け入れるように、ミニポート ドライバーを示します。 このマルチポートのデバイスでデバイスを識別する手段で暗黙的なあいまいさが意図的なものです。 HBA や、ファブリック、ベンダー固有の方法で、あいまいさを解決することができます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_CAN_BIND_TO_LUID</p></td>
<td align="left"><p>HBA の機能、および SCSI 問い合わせデータから派生した論理ユニットの id 記述子によってファイバー チャネルの論理ユニットを識別する永続的なバインドを受け入れるように、ミニポート ドライバーを示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_CAN_BIND_ANY_LUNS</p></td>
<td align="left"><p>オペレーティング システムとファイバー チャネルの論理ユニット番号の両方を指定する永続的なバインディング設定をそのまま使用するには、HBA の機能とそのミニポート ドライバーを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_CAN_BIND_TARGETS</p></td>
<td align="left"><p>論理ユニットのファイバー チャネル プロトコル (FCP) 識別子と、バスとターゲットなどの論理ユニットを識別するために、オペレーティング システムを使用する情報の永続的なバインディングを生成するには、HBA の機能とそのミニポート ドライバーを示します格納されている番号、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff556042" data-raw-source="[&lt;strong&gt;HBAScsiID&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556042)"> <strong>HBAScsiID</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_CAN_BIND_AUTOMAP</p></td>
<td align="left"><p>ターゲット マッピングと永続的なバインドの検出されたすべての記憶域リソースを自動的に生成するには、HBA の機能とそのミニポート ドライバーを示します。 この機能が反映されていませんまたは無効になっていますが、許可されている唯一のバインドの値は、オペレーティング システムで明示的に構成されているです。 バインドの明示的な構成には、論理ユニット番号 (LUN) のマスクが容易になります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_CAN_BIND_CONFIGURED</p></td>
<td align="left"><p>HBA の機能と永続的なバインディングの動的な構成を受け入れるように、ミニポート ドライバーを示します。</p></td>
</tr>
</tbody>
</table>

 

含めることによって*Hbaapi.h*ソフトウェアは、一連の前の表に、型名に対応するシンボリック定数へのアクセスになります。 これらの記号定数の定義が記載されていない*Hbapiwmi.h* (WMI ツールのスイートを生成、コンパイル時にファイル)。

 

 





