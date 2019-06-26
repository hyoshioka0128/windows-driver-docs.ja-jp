---
title: VMQ 用の標準化された INF キーワード
description: VMQ 用の標準化された INF キーワード
ms.assetid: 5DA92019-D2E0-41D9-9C31-94E464B824BA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f99f65e8e8cced968a0cbf3062541f60d12dad54
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378610"
---
# <a name="standardized-inf-keywords-for-vmq"></a>VMQ 用の標準化された INF キーワード


有効にするか、ネットワーク アダプターの仮想マシン キュー (VMQ) 機能のサポートを無効にするのには、次の標準化された INF キーワードが定義されています。

<a href="" id="-vmq"></a> **\*VMQ**  
デバイスが有効になっているまたは VMQ 機能を無効になっているかどうかを示す値。

<a href="" id="-vmqlookaheadsplit"></a> **\*VMQLookaheadSplit**  
先読みアサーションにバッファーおよび post lookahead バッファーに、デバイスが有効になっているまたは分割する機能を無効になっているかどうかを示す値が表示されます。 ミニポート ドライバー、NDIS を使用してこの機能の報告\_受信\_フィルター\_先読み\_分割\_でサポートされているフラグ、 **SupportedQueueProperties**メンバー、 [ **NDIS\_受信\_フィルター\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)構造体。 この機能の詳細については、次を参照してください。[受信バッファー内の共有メモリ](shared-memory-in-receive-buffers.md)します。

**注**NDIS 6.30 以降、パケット データを別の lookahead バッファーに分割することは現在サポートされていません。 Windows Server 2012 以降では、この INF キーワードは、廃止されています。



<a href="" id="-vmqvlanfiltering"></a> **\*VMQVlanFiltering**  
制御 (MAC) ヘッダーをデバイスが有効になっているまたはメディアで、VLAN 識別子を使用して、ネットワーク パケットをフィルター処理する機能を無効になっているかどうかを示す値にアクセスします。 ミニポート ドライバー、NDIS を使用してこの機能の報告\_受信\_フィルター\_MAC\_ヘッダー\_VLAN\_ID\_でサポートされているフラグ**SupportedMacHeaderFields**のメンバー、 [ **NDIS\_受信\_フィルター\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)構造体。

<a href="" id="-rssorvmqpreference"></a> **\*RssOrVmqPreference**  
代わりに VMQ 機能を有効にするかどうかを定義する値は受信側のスケーリング (RSS) 機能です。

これは、INF ファイルで指定する必要がありますいないに表示されていない非表示のキーワード値**詳細**ネットワーク アダプターのプロパティ ページ。 詳細については、次を参照してください。 [VMQ の処理と RSS INF キーワード](#vmq-rss)します。

VMQ に標準化された INF キーワードはキーワードを列挙します。 次の表では、VMQ に標準化された INF キーワードの可能な INF エントリについて説明します。

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
<td align="left"><p><strong><em>VMQ</strong></p></td>
<td align="left"><p>仮想マシン キュー</p></td>
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
<td align="left"><p><strong></em>VMQLookaheadSplit</strong></p></td>
<td align="left"><p>VMQ 先読みの分割</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>無効</p>
<div class="alert">
<strong>注</strong>NDIS 6.30 以降、このキーワードは現在サポートされていません。
</div>
<div>

</div></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 (既定)</p></td>
<td align="left"><p>有効</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>VMQVlanFiltering</strong></p></td>
<td align="left"><p>VMQ VLAN がフィルター処理</p></td>
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
<td align="left"><p><strong></em>RssOrVmqPreference</strong></p></td>
<td align="left"><p>注:このサブキーの ParamDesc と EnumDesc のエントリは、INF ファイルやユーザー インターフェイスのいずれかで使用できません。 詳細については、次を参照してください。 <a href="#vmq-rss" data-raw-source="[Handling VMQ and RSS INF Keywords](#vmq-rss)">VMQ の処理と RSS INF キーワード</a>します。</p></td>
<td align="left"><p>0 (既定)</p></td>
<td align="left"><div class="alert">
<strong>注</strong>RSS のレポート機能
</div>
<div>

</div></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><div class="alert">
<strong>注:</strong><br/><p>VMQ 機能のレポート</p>
</div>
<div>

</div></td>
</tr>
</tbody>
</table>



このテーブルの列には、列挙型のキーワードは次の属性について説明します。

<a href="" id="subkeyname"></a>SubkeyName  
INF ファイルで指定する必要があります、キーワードの名前。 この名前は、下のレジストリにも表示されます、 **NDI**\\**params**ネットワーク アダプターのキー。

<a href="" id="paramdesc"></a>ParamDesc  
SubkeyName INF エントリに関連付けられているテキスト。

**注**独立系ハードウェア ベンダー (IHV) は、SubkeyName のわかりやすいテキストを定義できます。



<a href="" id="value"></a>値  
一覧で各 SubkeyName に関連付けられている列挙型の整数値。

<a href="" id="enumdesc"></a>EnumDesc  
表示テキストで表示される各値に関連付けられている、 **詳細** プロパティ ページ。

標準化された INF キーワードの詳細については、次を参照してください。[ネットワーク デバイスの標準化された INF キーワード](standardized-inf-keywords-for-network-devices.md)します。

### <a href="" id="vmq-rss"></a>VMQ および RSS INF キーワードの処理

ネットワーク アダプターで VMQ をサポートし、受信側 scaling (RSS) は、これらの機能を同時に使用できません。 オペレーティング システムでは、次のように RSS または VMQ 機能の使用を有効にします。

-   TCP/IP スタックにネットワーク アダプターがバインドされると、オペレーティング システムは、RSS 機能を使用できるようにします。

-   ネットワーク アダプターが HYPER-V 拡張可能スイッチのドライバー スタックにバインドされると、オペレーティング システム、VMQ 機能の使用を有効にします。

    詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチ](hyper-v-extensible-switch.md)します。

いないネットワーク アダプターが無効になっているし、TCP/IP スタックからバインド解除され、HYPER-V ドライバー スタック (またはその逆) にバインドされているときに再有効化、ために VMQ および RSS の間で自動的に切り替えるには、このようなネットワーク アダプターのことはできません。

NDIS を呼び出すと、 [ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数、ミニポート ドライバーこれらの手順に従う NDIS に現在有効になっている VMQ または RSS 機能を報告する前に。

1.  ミニポート ドライバーの読み込み、  **\*RssOrVmqPreference** NDIS を現在有効になっている機能を報告する前にキーワード。

    場合の値、  **\*RssOrVmqPreference**キーワードが 1 の場合、ミニポート ドライバー VMQ の基本設定が構成されています。

    場合の値、  **\*RssOrVmqPreference**キーワードは、0 またはキーワードが存在しない、RSS の基本設定が構成されているミニポート ドライバー。

2.  それを読み取る必要があるかどうかミニポート ドライバーは VMQ の基本設定の構成で、  **\*VMQ**ネットワーク アダプターで VMQ が有効になっているかどうかを決定するキーワード。 キーワードが 1 に設定されている場合、ドライバーは VMQ 設定の現在対応を報告します。 ミニポート ドライバーで VMQ 設定を報告する方法の詳細については、次を参照してください。[ネットワーク アダプターの VMQ 機能を判断する](determining-the-vmq-capabilities-of-a-network-adapter.md)します。

    VMQ キーワードの詳細については、VMQ の標準化された INF キーワードを参照してください。

    **注**キーワードを標準化、RSS のいずれかを読み取り、ミニポート ドライバーでは VMQ の基本設定が構成されていると場合、いない必要があります。



3.  これを読み取る必要があるかどうかは、RSS の基本設定のミニポート ドライバーが構成されている、  **\*RSS**ネットワーク アダプターで RSS が有効になっているかどうかを決定するキーワード。 キーワードが 1 に設定されている場合、ドライバーは現在有効になっている RSS の設定を報告します。 ミニポート ドライバーが RSS の設定を報告する方法の詳細については、次を参照してください。 [RSS 構成](rss-configuration.md)します。

    RSS キーワードの詳細については、次を参照してください。[の RSS の標準化された INF キーワード](standardized-inf-keywords-for-rss.md)します。

    **注**キーワードを標準化、VMQ のいずれかを読み取り、ミニポート ドライバーでは RSS の基本設定が構成されていると場合、いない必要があります。



次の表には、ミニポート ドライバーの RSS または VMQ 設定の決定し、レジストリのキーワードを基に機能をアドバタイズがについて説明します。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><em>RssOrVmqPreference</th>
<th align="left"></em>VMQ</th>
<th align="left">\* RSS</th>
<th align="left">VMQ または RSS の機能を提供</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>なし</p></td>
<td align="left"><p>VMQ</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>なし</p></td>
<td align="left"><p>なし</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0 の場合、またはレジストリに存在しません</p></td>
<td align="left"><p>なし</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>RSS</p></td>
</tr>
<tr class="even">
<td align="left"><p>0 の場合、またはレジストリに存在しません</p></td>
<td align="left"><p>なし</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>なし</p></td>
</tr>
</tbody>
</table>



**注**ミニポート ドライバーは、完全な RSS および VMQ のハードウェアの機能をこれらのキーワードの値に関係なく常に報告する必要があります。 これらのキーワードの設定では、ドライバーが現在有効になっている RSS および VMQ 機能を報告する方法のみに影響します。



### <a name="reserved-registry-keywords"></a>レジストリの予約済みキーワード

ミニポート ドライバーは VMQ をサポートしているネットワーク アダプターで VMQ インターフェイスが有効になっている場合は、ドライバーが、次の RSS INF エントリを読み取れませんする必要があります。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">SubkeyName</th>
<th align="left">ParamDesc</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p></p>
<p><strong><em>RssMaxProcNumber</strong></p></td>
<td align="left"><p>RSS インターフェイスのプロセッサの最大数。</p></td>
<td align="left"><p>0 ~ (MAXIMUM_PROC_PER_GROUP-1)</p></td>
</tr>
<tr class="even">
<td align="left"><p></p>
<p><strong></em>MaxRssProcessors</strong></p></td>
<td align="left"><p>RSS プロセッサの最大数。</p></td>
<td align="left"><p>1 MAXIMUM_PROC_PER_SYSTEM ~。</p></td>
</tr>
</tbody>
</table>



VMQ をサポートしているミニポート ドライバーは、次のサブキーを読み取れませんする必要があります、 **HKEY\_ローカル\_マシン**\\**システム**\\ **CurrentControlSet**\\**サービス**\\**VMSMP**\\**パラメーター**レジストリキー。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">SubkeyName</th>
<th align="left">ParamDesc</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p></p>
<p><strong>TenGigVmqEnabled</strong></p></td>
<td align="left"><p>有効または、すべての 10 ギガビット (Gbps) の 2 つ目のネットワーク アダプターごとに VMQ を無効にします。</p></td>
<td align="left"><p>0 = システムの既定値 (Windows Server 2008 R2 を無効になっています)。</p>
<p>1 = 有効にします。</p>
<p>2 = 明示的に無効になっています。</p></td>
</tr>
<tr class="even">
<td align="left"><p></p>
<p><strong>BelowTenGigVmqEnabled</strong></p></td>
<td align="left"><p>有効または 10 Gbps 未満をサポートするすべてのネットワーク アダプターで VMQ が無効にします。</p></td>
<td align="left"><p>0 = システムの既定値 (Windows Server 2008 R2 を無効になっています)。</p>
<p>1 = 有効にします。</p>
<p>2 = 明示的に無効になっています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p></p>
<p><strong><em>RssMaxProcNumber</strong></p></td>
<td align="left"><p>RSS インターフェイスのプロセッサの最大数。</p></td>
<td align="left"><p>0 ~ (MAXIMUM_PROC_PER_GROUP-1)</p></td>
</tr>
<tr class="even">
<td align="left"><p></p>
<p><strong></em>MaxRssProcessors</strong></p></td>
<td align="left"><p>RSS プロセッサの最大数。</p></td>
<td align="left"><p>1 MAXIMUM_PROC_PER_SYSTEM ~。</p></td>
</tr>
</tbody>
</table>











