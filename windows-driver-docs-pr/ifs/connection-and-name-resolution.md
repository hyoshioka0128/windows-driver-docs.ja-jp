---
title: 接続と名前の解決
description: 接続と名前の解決
ms.assetid: e61d09f1-7951-4291-93ce-e5ccbe0be576
keywords:
- ミニリダイレクター WDK、接続
- ミニリダイレクター WDK、名前解決
- WDK ファイルシステムの名前
- WDK ミニリダイレクターの接続
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00755c7c89b763faa837c27fde5b6928ef454f91
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841460"
---
# <a name="connection-and-name-resolution"></a>接続と名前の解決


ネットワークミニリダイレクターは、リモートサーバーへの接続を確立し、いくつかのルーチンを使用して名前解決を処理します。 RDBSS は、このプロセスをいくつかの構造に抽象化します。これには、SRV\_呼び出し、NET\_ROOT、V\_NET\_ルート構造がカウントされます。 ネットワークミニリダイレクターの用語では、接続の確立が "ツリー接続" と呼ばれることがよくあります。 この接続を確立するには、SRV\_呼び出し、ネット\_ルート、および V\_NET\_ルート構造を作成する必要があります。 そのため、通常の手順は、ネットワークミニリダイレクター [**MRxCreateSrvCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_create_srvcall)ルーチンの呼び出しの後に、 [**MRxSrvCallWinnerNotify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_srvcall_winner_notify)ルーチンと[**MRxCreateVNetRoot**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_create_v_net_root)ルーチンを呼び出すことです。 これらの呼び出しは、通常、ユーザーモードのアプリケーションまたはサービスからの要求に応じて発行され、ドライブをマウントします (**net use x: \\\\サーバー\\パブリック**など)。 これらの呼び出しは、UNC ファイルオブジェクトの要求 (**メモ帳 \\\\server\\public\\readme.txt**など) によって発生することもあります。 RDBSS は、これらの両方のケースをネットワークミニリダイレクターの内部で処理し、 **MRxCreateSrvCall**シーケンスを開始します。

接続が削除されると、同様の finalize 呼び出しが行われ、SRV\_呼び出しと、NET\_ルート構造が破棄され、使用されているすべてのメモリが解放されます。 ネットワークミニリダイレクターに対するこれらの呼び出しには、 [**MRxFinalizeVNetRoot**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_finalize_v_net_root_calldown)、 [**MRxFinalizeNetRoot**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_finalize_net_root_calldown)、および[**MRxFinalizeSrvCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_finalize_srvcall_calldown)が含まれます。

RDBSS の元の設計では、さまざまなネットワークミニリダイレクターが RDBSS の1つのコピーを共有していましたが、これは実装されていませんでした。 この当初の設計の holdover は、さまざまなネットワークミニリダイレクターが、ネットワーク接続 (\\\\サーバー\\共有など) の要求を満たすために競合していることを示しています。 [**MRxSrvCallWinnerNotify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_srvcall_winner_notify)ルーチンは、複数のリダイレクターが要求を満たすことができた場合に、RDBSS がネットワークミニリダイレクターに通知するために使用されます。 優先順位の高いネットワークミニリダイレクターは、SRV\_呼び出しを作成し、サーバーとの接続を確立する必要があります。

Windows Server 2003、Windows XP、および Windows 2000 の RDBSS の実装では、各ネットワークミニリダイレクターに独自の RDBSS のコピーがあるため、RDBSS レイヤーに競合するネットワークリダイレクターは存在しません。 各ネットワークミニリダイレクター (ネットワークプロバイダー) と RDBSS のローカルコピーは、レジストリ設定の順序に基づいて順番に呼び出されます。プロバイダーが照会される順序は、次のレジストリ値によって制御されます。

```cpp
ProviderOrder
```

このレジストリ値は、次のレジストリキーの下にあります。

```cpp
HKLM\CurrentControlSet\Control\NetworkProvider\Order
```

[**MRxSrvCallWinnerNotify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_srvcall_winner_notify)ルーチンは、SRV\_呼び出し構造を作成するすべての要求の後に呼び出されます。

次の表に、接続と名前解決操作のためにネットワークミニリダイレクターで実装できるルーチンを示します。

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
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_create_srvcall" data-raw-source="[&lt;strong&gt;MRxCreateSrvCall&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_create_srvcall)"><strong>MRxCreateSrvCall</strong></a></td>
<td align="left"><p>RDBSS はこのルーチンを呼び出して、ネットワークミニリダイレクターが SRV_CALL 構造を作成し、サーバーとの接続を確立するように要求します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_create_v_net_root" data-raw-source="[&lt;strong&gt;MRxCreateVNetRoot&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_create_v_net_root)"><strong>MRxCreateVNetRoot</strong></a></td>
<td align="left"><p>RDBSS は、このルーチンを呼び出して、ネットワークミニリダイレクターが V_NET_ROOT 構造体を作成するように要求します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_extract_netroot_name" data-raw-source="[&lt;strong&gt;MRxExtractNetRootName&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_extract_netroot_name)"><strong>MRxExtractNetRootName</strong></a></td>
<td align="left"><p>RDBSS は、このルーチンを呼び出して、ネットワークミニリダイレクターが、指定されたパス名の NET_ROOT 構造から名前を抽出するように要求します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_finalize_net_root_calldown" data-raw-source="[&lt;strong&gt;MRxFinalizeNetRoot&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_finalize_net_root_calldown)"><strong>MRxFinalizeNetRoot</strong></a></td>
<td align="left"><p>RDBSS は、このルーチンを呼び出して、ネットワークミニリダイレクターが NET_ROOT オブジェクトを完了するように要求します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_finalize_srvcall_calldown" data-raw-source="[&lt;strong&gt;MRxFinalizeSrvCall&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_finalize_srvcall_calldown)"><strong>MRxFinalizeSrvCall</strong></a></td>
<td align="left"><p>RDBSS は、このルーチンを呼び出して、サーバーとの接続確立に使用される SRV_CALL 構造をネットワークミニリダイレクターが完了するように要求します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_finalize_v_net_root_calldown" data-raw-source="[&lt;strong&gt;MRxFinalizeVNetRoot&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_finalize_v_net_root_calldown)"><strong>MRxFinalizeVNetRoot</strong></a></td>
<td align="left"><p>RDBSS は、このルーチンを呼び出して、ネットワークミニリダイレクターが V_NET_ROOT 構造を完了するように要求します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_preparse_name" data-raw-source="[&lt;strong&gt;MRxPreparseName&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_preparse_name)"><strong>MRxPreparseName</strong></a></td>
<td align="left"><p>RDBSS はこのルーチンを呼び出して、ネットワークミニリダイレクターに名前を preparse する機会を与えます。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_srvcall_winner_notify" data-raw-source="[&lt;strong&gt;MRxSrvCallWinnerNotify&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_srvcall_winner_notify)"><strong>MRxSrvCallWinnerNotify</strong></a></td>
<td align="left"><p>このルーチンは、RDBSS によって呼び出されるように設計されており、複数のリダイレクターが要求を満たすことができるようになったことをネットワークミニリダイレクターに通知します。 優先されるネットワークミニリダイレクターは、SRV_CALL 構造を作成し、サーバーとの接続を確立する必要があります。</p>
<p>RDBSS の現在の実装では、各ネットワークミニリダイレクターは RDBSS の独自のコピーを持っているため、RDBSS 層で競合するネットワークリダイレクターは存在しません。 このルーチンは、SRV_CALL 構造体を作成するすべての要求の前に呼び出されます。</p>
<p>同じ UNC 名前空間を処理するために複数のリダイレクターがインストールされている場合、要求を処理するリダイレクターは、レジストリに指定されているリダイレクターの順序に基づいて、MUP によって選択されます。</p></td>
</tr>
</tbody>
</table>

 

 

 




