---
title: RSS 用の標準化された INF キーワード
description: RSS 用の標準化された INF キーワード
ms.assetid: 0ea0d6f7-0dc5-40dd-a706-4712e19dbfdb
keywords:
- 受信側のスケーリング WDK ネットワー キングに標準化された INF キーワード
- ネットワーク、RSS WDK に標準化された INF キーワード
- 標準化された INF キーワード WDK RSS
- INF エントリ WDK RSS
ms.date: 02/01/2019
ms.localizationpriority: medium
ms.openlocfilehash: 2678acbbcda42f5afd9dc6a80f8e936ec15fd421
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378626"
---
# <a name="standardized-inf-keywords-for-rss"></a>RSS 用の標準化された INF キーワード

インターフェイスのサポートの RSS [INF キーワードを標準化](standardized-inf-keywords-for-network-devices.md)をレジストリに表示され、INF ファイルで指定されます。

次に示します列挙[INF キーワードを標準化](standardized-inf-keywords-for-network-devices.md)rss:

<a href="" id="---------rss"></a> **\*RSS**  
有効またはミニポート アダプター用の RSS のサポートを無効にします。

<a href="" id="---------rssprofile"></a> **\*RSSProfile**  
プロセッサの選択とプロファイルの負荷分散します。

**注**  への変更、  **\*RSSProfile**設定には、アダプターの再起動が必要とします。

 

列挙に標準化された INF キーワードは、次の属性を指定します。

<a href="" id="subkeyname"></a>SubkeyName  
レジストリ内の INF ファイルに指定する必要があります、キーワードの名前が表示されます。

<a href="" id="paramdesc"></a>ParamDesc  
SubkeyName に関連付けられているテキスト。

<a href="" id="value"></a>値  
リスト内の各オプションに関連付けられている列挙の整数値。 この値は NDI\\params\\ *SubkeyName*\\*値*します。

<a href="" id="enumdesc"></a>EnumDesc  
メニューに表示される各値に関連付けられている表示テキスト。

<a href="" id="default"></a>既定値  
メニューの既定値。

次の表では、キーワードの場合、RSS の列挙可能な INF エントリについて説明します。

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
<td align="left"><p><strong><em>RSS</strong></p></td>
<td align="left"><p>Receive Side Scaling</p></td>
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
<td align="left"><p><strong></em>RSSProfile</strong></p></td>
<td align="left"><p>RSS は負荷分散プロファイル</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p><strong>ClosestProcessor</strong>:既定の動作は、一貫性のある Windows Server 2008 R2 のです。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p><strong>ClosestProcessorStatic</strong>:ない動的負荷分散の配布が実行時の負荷はありません。</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3</p></td>
<td align="left"><p><strong>NUMAScaling</strong>:ラウンド ロビン方式で規模をうまく調整 NUMA サーバー上で実行されているアプリケーションを有効にするには、各 NUMA ノード間での RSS Cpu を割り当てます。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>4</p>
<p>EnterprisePublishing</p></td>
<td align="left"><p><strong>NUMAScalingStatic</strong>:RSS プロセッサの選択は、NUMA スケーラビリティ動的負荷分散なしの場合と同じです。</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>5</p></td>
<td align="left"><p><strong>ConservativeScaling</strong>:RSS は、できるだけ少ないプロセッサを使用して、負荷に対応します。 このオプションは、割り込みの数を減らすのに役立ちます。</p></td>
</tr>
</tbody>
</table>

 

NDIS 6.30 サポートが追加されました **\*RSSProfile**します。

次の一覧表示されます、 [INF キーワードを標準化](standardized-inf-keywords-for-network-devices.md)の編集可能な RSS:

<a href="" id="---------rssbaseprocgroup"></a> **\*RssBaseProcGroup**  
指定されているプロセッサ数のプロセッサ グループの数、  **\*RssBaseProcNumber**キーワード。

<a href="" id="---------numanodeid"></a> **\*NumaNodeId**  
ネットワーク アダプターのメモリ割り当てに使用される優先 NUMA ノード。 また、オペレーティング システムが最初の RSS、優先 NUMA ノードから、Cpu を使用しようとします。

PCI 拡張カードのドライバーでは、NUMA ノードに接続されているため、最も近いノードがどの PCI スロットにカードを依存の INF に静的に ID を指定しないでください。  指定のみ **\*NumaNodeId**かどうか、ネットワーク アダプターは、システムに統合されて、NUMA ノードは、事前に既知のおよびノードは、ACPI をクエリすることによって実行時に決定できません。

**注**  NDIS がこの値を使用してこのキーワードが存在し、その値が、コンピューターの NUMA ノード数より小さい場合、 **PreferredNumaNode**内のメンバー、 [ **NDIS\_RSS\_プロセッサ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_rss_processor_info)構造体。

 

**注**  Windows 8 で、  **\*NumaNodeId** NIC RSS プロファイルに設定されている場合、値は無視されます**NUMAScaling**(2) または**NUMAScalingStatic**(3)。

 

<a href="" id="---------rssbaseprocnumber"></a> **\*RssBaseProcNumber**  
指定したグループ内の基本の RSS プロセッサの数。

<a href="" id="---------maxrssprocessors"></a> **\*MaxRssProcessors**  
RSS プロセッサの最大数。

<a href="" id="---------rssmaxprocnumber"></a> **\*RssMaxProcNumber**  
RSS インターフェイスのプロセッサの最大数。
場合 **\*RssMaxProcNumber**が指定されると、  **\*RssMaxProcGroup**も指定する必要があります。

<a href="" id="---------rssmaxprocnumber"></a> **\*NumRSSQueues**  
RSS のキューの数。

<a href="" id="---------rssmaxprocgroup"></a> **\*RssMaxProcGroup** RSS インターフェイスの最大のプロセッサ グループ。

**\*RssBaseProcGroup**と共に **\*RssBaseProcNumber** RSS で使用できる最小のプロセッサ数を識別する PROCESSOR_NUMBER 構造を形成します。
**\*RssMaxProcGroup**と共に **\*RssMaxProcNumber** RSS で使用できるプロセッサの最大数を識別する PROCESSOR_NUMBER 構造を形成します。

たとえば、  **\*RssBaseProcGroup**を 1 に設定されている **\*RssBaseProcNumber** 16 に設定されている **\*RssMaxProcGroup**は3 に設定し、  **\*RssMaxProcNumber** 8 に設定されます。
使用して<group>:<processor>表記では、基本のプロセッサが 1時 16分と max のプロセッサが 3:8。
プロセッサ 0:0, 0:32、1:0 と 1時 15分は反映されません、RSS の候補となる基本プロセッサ数を下回っているためです。
プロセッサ 1:16、2:0、1: 31 2:63、3:0、および 3:8 はすべてと見なさ RSS の候補となる 3:8 までの範囲 1時 16分になったためです。
3:9 のプロセッサが候補と見なされない rss、プロセッサの最大数を超えているため、3:31、および 4:0。

NDIS 6.20 サポートが追加されました、  **\*RssBaseProcGroup**、  **\*NumaNodeId**、  **\*RssBaseProcNumber**、および **\*MaxRssProcessors**キーワード。

NDIS 6.30 サポートが追加されました、  **\*RssMaxProcNumber**、および **\*NumRSSQueues**キーワード。

[INF キーワードを標準化](standardized-inf-keywords-for-network-devices.md)を編集できる次の属性します。

<a href="" id="subkeyname"></a>SubkeyName  
レジストリ内の INF ファイルに指定する必要があります、キーワードの名前が表示されます。

<a href="" id="paramdesc"></a>ParamDesc  
SubkeyName に関連付けられているテキスト。

<a href="" id="type"></a>型  
編集可能な値の型。 いずれかの値を指定できます (Int) の数値 (編集) を編集することができるテキストまたは。

<a href="" id="default-value"></a>既定値  
整数またはテキストの既定値。 &lt;定義されている IHV&gt;値が特定の独立系ハードウェア ベンダー (IHV) の要件に関連付けられていることを示します。

<a href="" id="min"></a>最小値  
整数値が許容される最小値。 &lt;定義されている IHV&gt;最小値が特定の IHV 要件に関連付けられていることを示します。

<a href="" id="max"></a>最大  
整数値で許可される最大値。 &lt;定義されている IHV&gt;最小値が特定の IHV 要件に関連付けられていることを示します。

次の表では、すべての編集可能な RSS キーワードについて説明します。

<table style="width:100%;">
<colgroup>
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">SubkeyName</th>
<th align="left">ParamDesc</th>
<th align="left">型</th>
<th align="left">既定値</th>
<th align="left">最小</th>
<th align="left">最大</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em>RssBaseProcGroup</strong></p></td>
<td align="left"><p>RSS ベースのプロセッサ グループ</p></td>
<td align="left"><p>整数</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>MAXIMUM_GROUPS 1</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em>NumaNodeId</strong></p></td>
<td align="left"><p>優先 NUMA ノード</p></td>
<td align="left"><p>整数</p></td>
<td align="left"><p>65535 (任意のノード)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>システムに固有の 65534 を超えることはできません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>RssBaseProcNumber</strong></p></td>
<td align="left"><p>RSS ベースのプロセッサ数</p></td>
<td align="left"><p>整数</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>MAXIMUM_PROC_PER_GROUP 1</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em>MaxRssProcessors</strong></p></td>
<td align="left"><p>RSS プロセッサの最大数</p></td>
<td align="left"><p>整数</p></td>
<td align="left"><p>Windows Server 2008 の既定値:</p>
<p>1 G または低速アダプター, 16 10 G アダプター、8</p>
<p>Windows 8 の既定値:</p>
<p>Nic のなし、MSI X のサポート - 2 の 1 gbe または 10 GbE アダプターを 4、低速のアダプター。</p>
<p>MSI X のサポート - 4 の 1 gbe または 10 GbE アダプターの 16、低速のアダプターと nic の。</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>MAXIMUM_PROC_PER_SYSTEM</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>RssMaxProcNumber</strong></p></td>
<td align="left"><p>RSS の最大プロセッサ数</p></td>
<td align="left"><p>整数</p></td>
<td align="left"><p>MAXIMUM_PROC_PER_GROUP 1 (既定)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>MAXIMUM_PROC_PER_GROUP 1</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em>NumRSSQueues</strong></p></td>
<td align="left"><p>RSS のキューの最大数</p></td>
<td align="left"><p>整数</p></td>
<td align="left"><p>デバイスに固有</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>デバイスに固有</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>*RSSMaxProcGroup</strong></p></td>
<td align="left"><p>RSS の最大プロセッサ グループ</p></td>
<td align="left"><p>整数</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>MAXIMUM_GROUPS 1</p></td>
</tr>
</tbody>
</table>

 

**注**  がの有効な範囲 **\*RssBaseProcGroup**が最大値に 0 です\_グループ 1 では、Windows 7 のゼロをある必要があります。 それ以外の場合、TCP/IP プロトコルを RSS のすべてのプロセッサを使用しません。

 

**注**  の既定値 **\*NumaNodeId** (65535) 手段、ネットワーク アダプターは、NUMA ノードに依存しないと、NDIS は別の任意のノードを使用しようとはしないでください。
場合、  **\*NumaNodeId**キーワードが存在し、NDIS ACPI からヒントに基づいて、最も近いノードを自動的に選択します。


標準化された INF キーワードの詳細については、次を参照してください。[ネットワーク デバイスの標準化された INF キーワード](standardized-inf-keywords-for-network-devices.md)します。

 

 





