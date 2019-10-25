---
title: VMQ 用の標準化された INF キーワード
description: VMQ 用の標準化された INF キーワード
ms.assetid: 5DA92019-D2E0-41D9-9C31-94E464B824BA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: af4c628c3aee9507c53b9411c813cd3a7f10a401
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841841"
---
# <a name="standardized-inf-keywords-for-vmq"></a>VMQ 用の標準化された INF キーワード


次の標準化された INF キーワードは、ネットワークアダプターの仮想マシンキュー (VMQ) 機能のサポートを有効または無効にするために定義されています。

<a href="" id="-vmq"></a> **\*VMQ**  
デバイスで VMQ 機能が有効または無効になっているかどうかを示す値。

<a href="" id="-vmqlookaheadsplit"></a> **\*Vmqlook Aヘッド分割**  
デバイスが受信バッファーを先読みバッファーと先読みバッファーに分割する機能を有効または無効にしたかどうかを示す値。 この機能は、ミニポートドライバーによって、NDIS\_受信\_\_\_フィルターを使用して報告されます。このフラグは、Ndis\_RECEIVE\_FILTER の**Supportedqueueproperties**メンバーにあります。 [**機能の構造 (__)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities) 。 この機能の詳細については、「[受信バッファーの共有メモリ](shared-memory-in-receive-buffers.md)」を参照してください。

**メモ** NDIS 6.30 以降では、パケットデータを個別の先読みバッファーに分割することはサポートされなくなりました。 Windows Server 2012 以降では、この INF キーワードは廃止されました。



<a href="" id="-vmqvlanfiltering"></a> **\*VMQVlanFiltering**  
メディアアクセス制御 (MAC) ヘッダーの VLAN 識別子を使用して、ネットワークパケットをフィルター処理する機能がデバイスで有効になっているか無効になっているかを示す値。 ミニポートドライバーは、この機能を NDIS\_受信\_フィルター\_MAC\_ヘッダー\_、Ndis の**SupportedMacHeaderFields**メンバーでサポートされているフラグ\_受信します。 [ **\_フィルター\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)の構造です。

<a href="" id="-rssorvmqpreference"></a>**RssOrVmqPreference の\***  
Receive side scaling (RSS) 機能の代わりに VMQ 機能を有効にする必要があるかどうかを定義する値。

これは、INF ファイルで指定することができず、ネットワークアダプターの **[詳細設定**] プロパティページには表示されない、非表示のキーワード値です。 詳細については、「 [VMQ と RSS の INF キーワードの処理](#vmq-rss)」を参照してください。

VMQ の標準化された INF キーワードは列挙キーワードです。 次の表では、VMQ の標準化された INF キーワードに使用できる INF エントリについて説明します。

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
<th align="left">Value</th>
<th align="left">EnumDesc</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em>VMQ</strong></p></td>
<td align="left"><p>仮想マシンのキュー</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>無効</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 (既定値)</p></td>
<td align="left"><p>有効</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>Vmqlook Aヘッド分割</strong></p></td>
<td align="left"><p>VMQ の先読み分割</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>無効</p>
<div class="alert">
<strong>メモ</strong> NDIS 6.30 以降では、このキーワードはサポートされなくなりました。
</div>
<div>

</div></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 (既定値)</p></td>
<td align="left"><p>有効</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>VMQVlanFiltering</strong></p></td>
<td align="left"><p>VMQ VLAN フィルター処理</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>無効</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 (既定値)</p></td>
<td align="left"><p>有効</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RssOrVmqPreference の</em></strong></p></td>
<td align="left"><p>注: このサブキーの ParamDesc および EnumDesc エントリは、INF ファイルでもユーザーインターフェイスでも使用できません。 詳細については、「 <a href="#vmq-rss" data-raw-source="[Handling VMQ and RSS INF Keywords](#vmq-rss)">VMQ と RSS の INF キーワードの処理</a>」を参照してください。</p></td>
<td align="left"><p>0 (既定値)</p></td>
<td align="left"><div class="alert">
<strong>メモ</strong> RSS 機能を報告する
</div>
<div>

</div></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><div class="alert">
<strong>注:</strong><br/><p>VMQ 機能を報告する</p>
</div>
<div>

</div></td>
</tr>
</tbody>
</table>



この表の列では、列挙型キーワードの次の属性について説明します。

<a href="" id="subkeyname"></a>SubkeyName  
INF ファイルで指定する必要があるキーワードの名前。 この名前は、ネットワークアダプターの**Ndi**\\**params**キーの下のレジストリにも表示されます。

<a href="" id="paramdesc"></a>ParamDesc  
SubkeyName INF エントリに関連付けられている表示テキスト。

**メモ** 独立系ハードウェアベンダー (IHV) は、SubkeyName の説明文を定義できます。



<a href="" id="value"></a>数値  
リスト内の各 SubkeyName に関連付けられている列挙整数値。

<a href="" id="enumdesc"></a>EnumDesc  
**詳細**プロパティページに表示される各値に関連付けられている表示テキスト。

標準化された INF キーワードの詳細については、「[ネットワークデバイスの標準化](standardized-inf-keywords-for-network-devices.md)された inf キーワード」を参照してください。

### <a href="" id="vmq-rss"></a>VMQ と RSS の INF キーワードの処理

VMQ と receive side scaling (RSS) をサポートするネットワークアダプターでは、これらの機能を同時に使用することはできません。 オペレーティングシステムでは、RSS または VMQ 機能を次のように使用できます。

-   ネットワークアダプターが TCP/IP スタックにバインドされている場合、この動作により RSS 機能を使用できるようになります。

-   ネットワークアダプターが Hyper-v 拡張可能スイッチドライバースタックにバインドされている場合、オペレーティングシステムは VMQ 機能を使用できるようになります。

    詳細については、「 [Hyper-v 拡張可能スイッチ](hyper-v-extensible-switch.md)」を参照してください。

ネットワークアダプターは無効にされておらず、TCP/IP スタックからバインドが解除され、Hyper-v ドライバースタック (またはその逆) にバインドされている場合に再び有効になるため、このようなネットワークアダプターで VMQ と RSS を自動的に切り替えることはできません。

NDIS が[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数を呼び出すと、ミニポートドライバーは、現在有効になっている VMQ または RSS 機能を ndis に報告する前に、次の手順に従います。

1.  ミニポートドライバーは、現在有効になっている機能を NDIS に報告する前に、 **\*RssOrVmqPreference**キーワードを読み取ります。

    **\*RssOrVmqPreference**キーワードの値が1の場合、ミニポートドライバーは VMQ 優先順位用に構成されています。

    **\*RssOrVmqPreference**キーワードの値が0であるか、キーワードが存在しない場合、ミニポートドライバーは RSS 設定用に構成されます。

2.  ミニポートドライバーが VMQ 優先用に構成されている場合、ネットワークアダプターで VMQ が有効になっているかどうかを確認するには、 **\*vmq**キーワードを読み取る必要があります。 キーワードが1に設定されている場合は、現在有効になっている VMQ の設定がドライバーによって報告されます。 ミニポートドライバーが VMQ 設定を報告する方法の詳細については、「[ネットワークアダプターの Vmq 機能の決定](determining-the-vmq-capabilities-of-a-network-adapter.md)」を参照してください。

    VMQ キーワードの詳細については、「VMQ の標準化された INF キーワード」を参照してください。

    **メモ** ミニポートドライバーが VMQ 設定用に構成されている場合、RSS の標準化されたキーワードを読み取ることはできません。



3.  ミニポートドライバーが RSS 設定用に構成されている場合は、ネットワークアダプターで RSS が有効になっているかどうかを確認するために、 **\*の rss**キーワードを読み取る必要があります。 キーワードが1に設定されている場合は、現在有効になっている RSS 設定がドライバーによって報告されます。 ミニポートドライバーが RSS 設定を報告する方法の詳細については、「 [rss の構成](rss-configuration.md)」を参照してください。

    RSS キーワードの詳細については、「 [rss 用の標準化](standardized-inf-keywords-for-rss.md)された INF キーワード」を参照してください。

    **メモ** ミニポートドライバーが RSS 設定用に構成されている場合は、VMQ の標準化されたキーワードを読み取ることはできません。



次の表は、ミニポートドライバーが RSS または VMQ の設定を決定し、レジストリキーワードに基づいて機能をアドバタイズする方法を示しています。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">RssOrVmqPreference の <em></th>
<th align="left"></em>VMQ</th>
<th align="left">\* RSS</th>
<th align="left">提供される VMQ または RSS 機能</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>該当なし</p></td>
<td align="left"><p>VMQ</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>該当なし</p></td>
<td align="left"><p>なし</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0、またはレジストリに存在しません。</p></td>
<td align="left"><p>該当なし</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>RSS</p></td>
</tr>
<tr class="even">
<td align="left"><p>0、またはレジストリに存在しません。</p></td>
<td align="left"><p>該当なし</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>なし</p></td>
</tr>
</tbody>
</table>



**メモ** ミニポートドライバーは、これらのキーワードの値に関係なく、RSS および VMQ の完全なハードウェア機能を常に報告する必要があります。 これらのキーワードの設定は、ドライバーが現在有効になっている RSS および VMQ 機能を報告する方法にのみ影響します。



### <a name="reserved-registry-keywords"></a>予約済みレジストリキーワード

ミニポートドライバーで VMQ がサポートされており、ネットワークアダプターで VMQ インターフェイスが有効になっている場合、ドライバーは次の RSS INF エントリを読み取ることができません。

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
<td align="left"><p>0から (MAXIMUM_PROC_PER_GROUP-1)、</p></td>
</tr>
<tr class="even">
<td align="left"><p></p>
<p><strong></em>MaxRssProcessors</strong></p></td>
<td align="left"><p>RSS プロセッサの最大数。</p></td>
<td align="left"><p>1から MAXIMUM_PROC_PER_SYSTEM。</p></td>
</tr>
</tbody>
</table>



VMQ をサポートするミニポートドライバーは、 **HKEY\_ローカル\_コンピューター**\\**システム**\\**CurrentControlSet**\\**services**\\**VMSMP**の下にある次のサブキーを読み取ることはできません。\\**Parameters**レジストリキー。

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
<td align="left"><p>10ギガビット/秒 (Gbps) のネットワークアダプターで VMQ を有効または無効にします。</p></td>
<td align="left"><p>0 = システムの既定値 (Windows Server 2008 R2 では無効)。</p>
<p>1 = 有効。</p>
<p>2 = 明示的に無効にします。</p></td>
</tr>
<tr class="even">
<td align="left"><p></p>
<p><strong>BelowTenGigVmqEnabled</strong></p></td>
<td align="left"><p>10 Gbps 未満をサポートするすべてのネットワークアダプターで VMQ を有効または無効にします。</p></td>
<td align="left"><p>0 = システムの既定値 (Windows Server 2008 R2 では無効)。</p>
<p>1 = 有効。</p>
<p>2 = 明示的に無効にします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p></p>
<p><strong><em>RssMaxProcNumber</strong></p></td>
<td align="left"><p>RSS インターフェイスのプロセッサの最大数。</p></td>
<td align="left"><p>0から (MAXIMUM_PROC_PER_GROUP-1)、</p></td>
</tr>
<tr class="even">
<td align="left"><p></p>
<p><strong></em>MaxRssProcessors</strong></p></td>
<td align="left"><p>RSS プロセッサの最大数。</p></td>
<td align="left"><p>1から MAXIMUM_PROC_PER_SYSTEM。</p></td>
</tr>
</tbody>
</table>











