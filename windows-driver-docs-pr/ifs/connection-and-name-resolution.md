---
title: 接続と名前の解決
description: 接続と名前の解決
ms.assetid: e61d09f1-7951-4291-93ce-e5ccbe0be576
keywords:
- ミニ リダイレクター WDK、接続
- ミニ リダイレクター WDK、名前解決
- WDK の名前のファイル システム
- WDK のミニ リダイレクターの接続
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08a0ef58bcf2b978e8e4444187c33cba4db00768
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378986"
---
# <a name="connection-and-name-resolution"></a>接続と名前の解決


ネットワークのミニ リダイレクターは、リモート サーバーへの接続を確立し、いくつかのルーチンを使用する名前解決を処理します。 RDBSS、SRV を含むいくつかの構造にこのプロセスを抽象化\_呼び出し、NET\_ルート、および V\_NET\_カウントされた参照であるルート構造体。 ネットワーク ミニ リダイレクターには、接続の確立は多くの場合と呼ばれる、「ツリーに接続します」 この接続の確立、SRV を作成する必要が\_呼び出し、NET\_ルート、および V\_NET\_ルート構造体。 ネットワークのミニ リダイレクターを呼び出し、通常の手順となるように[ **MRxCreateSrvCall** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_create_srvcall)ルーチンへの呼び出し後に、 [ **MRxSrvCallWinnerNotify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_srvcall_winner_notify)と[ **MRxCreateVNetRoot** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_create_v_net_root)ルーチン。 これらの呼び出しは通常はドライブをマウントするには、ユーザー モード アプリケーションまたはサービスからの要求に対する応答で発行される (**net を使用して、x: \\ \\server\\パブリック**など)。 これらの呼び出しは、UNC ファイル オブジェクトの要求からも可能性 (**メモ帳\\ \\server\\パブリック\\readme.txt**など)。 RDBSS ミニリダイレクター ネットワークの内部でこのような場合の両方を処理し、開始、 **MRxCreateSrvCall**シーケンス。

接続が削除された、似たようなときの最終処理、SRV 破棄する呼び出しが行われる\_呼び出し、および NET\_構造のルートし、使用されているメモリを解放します。 ネットワークのミニ リダイレクターにこれらの呼び出しを含める[ **MRxFinalizeVNetRoot**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_finalize_v_net_root_calldown)、 [ **MRxFinalizeNetRoot**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_finalize_net_root_calldown)、および[**MRxFinalizeSrvCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_finalize_srvcall_calldown)します。

RDBSS の元のデザインは、さまざまなネットワーク ミニ リダイレクターがすべて共有 RDBSS の 1 つのコピーが、これが実装されていませんでした。 この元の設計からの保持は、さまざまなネットワーク ミニ リダイレクターがネットワーク接続の要求を満たすために競争力 (\\\\server\\を共有)。 [ **MRxSrvCallWinnerNotify** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_srvcall_winner_notify)ルーチンは、優先されたデータが複数リダイレクターは、要求を達成できますが、ネットワークのミニ リダイレクターに通知する RDBSS によって使用されます。 優先ネットワーク ミニリダイレクターは SRV を作成するが必要です。\_を呼び出すし、サーバーとの接続を確立します。

Windows Server 2003、Windows XP、および Windows 2000 で RDBSS の実装では、各ネットワーク ミニリダイレクターは、RDBSS 層でネットワーク リダイレクターの競合がないため RDBSS の独自のコピーが。 各ネットワーク ミニリダイレクター (ネットワーク プロバイダー) と RDBSS のローカル コピーはに基づいて呼び出される順番レジストリ設定の順序。プロバイダーが照会されます順序は、次のレジストリ値によって制御されます。

```cpp
ProviderOrder
```

このレジストリ値は、次のレジストリ キーの下にあります。

```cpp
HKLM\CurrentControlSet\Control\NetworkProvider\Order
```

[ **MRxSrvCallWinnerNotify** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_srvcall_winner_notify) 、SRV を作成するすべての要求後に呼び出されるルーチン\_呼び出し構造体。

次の表では、接続と名前解決操作のネットワーク ミニ リダイレクターで実装できるルーチンを示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ルーチン</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_create_srvcall" data-raw-source="[&lt;strong&gt;MRxCreateSrvCall&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_create_srvcall)"><strong>MRxCreateSrvCall</strong></a></td>
<td align="left"><p>RDBSS では、要求ネットワークのミニ リダイレクターが SRV_CALL 構造を作成し、サーバーとの接続を確立するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_create_v_net_root" data-raw-source="[&lt;strong&gt;MRxCreateVNetRoot&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_create_v_net_root)"><strong>MRxCreateVNetRoot</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターが V_NET_ROOT 構造を作成することを要求するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_extract_netroot_name" data-raw-source="[&lt;strong&gt;MRxExtractNetRootName&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_extract_netroot_name)"><strong>MRxExtractNetRootName</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターが指定したパス名の NET_ROOT 構造から名を抽出することを要求するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_finalize_net_root_calldown" data-raw-source="[&lt;strong&gt;MRxFinalizeNetRoot&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_finalize_net_root_calldown)"><strong>MRxFinalizeNetRoot</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターが NET_ROOT オブジェクトをファイナライズすることを要求するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_finalize_srvcall_calldown" data-raw-source="[&lt;strong&gt;MRxFinalizeSrvCall&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_finalize_srvcall_calldown)"><strong>MRxFinalizeSrvCall</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクター、ファイナライズ SRV_CALL 構造体がサーバーとの接続を確立するために使用されることを要求するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_finalize_v_net_root_calldown" data-raw-source="[&lt;strong&gt;MRxFinalizeVNetRoot&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_finalize_v_net_root_calldown)"><strong>MRxFinalizeVNetRoot</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクター V_NET_ROOT 構造の最終処理を要求するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_preparse_name" data-raw-source="[&lt;strong&gt;MRxPreparseName&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_preparse_name)"><strong>MRxPreparseName</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクター preparse 名をする機会を提供するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_srvcall_winner_notify" data-raw-source="[&lt;strong&gt;MRxSrvCallWinnerNotify&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_srvcall_winner_notify)"><strong>MRxSrvCallWinnerNotify</strong></a></td>
<td align="left"><p>このルーチンは、優勝者が複数リダイレクターは、要求を達成できますが、ネットワークのミニ リダイレクターに通知する RDBSS によって呼び出されるもともと設計されています。 SRV_CALL 構造を作成し、サーバーとの接続を確立するには、優先ネットワーク ミニリダイレクターが予定です。</p>
<p>RDBSS の現在の実装では、各ネットワーク ミニ-リダイレクターは、RDBSS 層でネットワーク リダイレクターの競合がないために、RDBSS の独自のコピーが。 このルーチンは、すべての要求 SRV_CALL 構造を作成する前に呼び出されます。</p>
<p>同じ UNC 名前空間を処理するため複数リダイレクターがインストールされると、要求をリダイレクターがリダイレクターが、レジストリで指定された順序に基づいて MUP によって選択されます。</p></td>
</tr>
</tbody>
</table>

 

 

 




