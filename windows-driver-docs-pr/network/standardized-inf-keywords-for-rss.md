---
title: RSS 用の標準化された INF キーワード
description: RSS 用の標準化された INF キーワード
ms.assetid: 0ea0d6f7-0dc5-40dd-a706-4712e19dbfdb
keywords:
- 受信側のスケーリング WDK ネットワーク、標準化された INF キーワード
- RSS WDK ネットワーク、標準化された INF キーワード
- 標準化された INF キーワード WDK RSS
- INF エントリ WDK RSS
ms.date: 02/01/2019
ms.localizationpriority: medium
ms.openlocfilehash: c6d17bfbe443d27fc640901ca5387d71296f49ca
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841838"
---
# <a name="standardized-inf-keywords-for-rss"></a>RSS 用の標準化された INF キーワード

RSS インターフェイスは、レジストリに表示され、INF ファイルで指定されている標準化された[inf キーワード](standardized-inf-keywords-for-network-devices.md)をサポートしています。

RSS の列挙型の標準化された[INF キーワード](standardized-inf-keywords-for-network-devices.md)を次に示します。

<a href="" id="---------rss"></a> **\*RSS**  
ミニポートアダプターの RSS のサポートを有効または無効にします。

<a href="" id="---------rssprofile"></a> **\*RSSProfile**  
プロセッサの選択と負荷分散プロファイル。

**\*RSSProfile**設定の変更には、アダプターの再起動が必要である**ことに注意**してください  。

 

列挙型の標準化された INF キーワードには、次の属性があります。

<a href="" id="subkeyname"></a>SubkeyName  
INF ファイルで指定する必要があり、レジストリに表示されるキーワードの名前。

<a href="" id="paramdesc"></a>ParamDesc  
SubkeyName に関連付けられている表示テキスト。

<a href="" id="value"></a>数値  
リスト内の各オプションに関連付けられている列挙整数値。 この値は、NDI\\params\\ *Subkeyname*\\*値*に格納されます。

<a href="" id="enumdesc"></a>EnumDesc  
メニューに表示される各値に関連付けられている表示テキスト。

<a href="" id="default"></a>標準  
メニューの既定値。

次の表では、RSS 列挙キーワードに使用できる INF エントリについて説明します。

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
<td align="left"><p><strong><em>RSS</strong></p></td>
<td align="left"><p>Receive Side Scaling</p></td>
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
<td align="left"><p><strong></em>RSSProfile</strong></p></td>
<td align="left"><p>RSS 負荷分散プロファイル</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p><strong>Closestprocessor</strong>: 既定の動作は、Windows Server 2008 R2 と同じです。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p><strong>Closestprocessorstatic</strong>: 動的負荷分散はありませんが、実行時の負荷分散は行われません。</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3</p></td>
<td align="left"><p><strong>Numascaling</strong>: すべての numa ノードで RSS cpu をラウンドロビン方式で割り当てて、numa サーバー上で実行されているアプリケーションを適切にスケーリングできるようにします。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>ホーム フォルダーが置かれているコンピューターにアクセスできない</p>
<p>EnterprisePublishing</p></td>
<td align="left"><p><strong>Numascalingstatic</strong>: RSS プロセッサの選択は、動的な負荷分散を使用しない NUMA スケーラビリティの場合と同じです。</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>5</p></td>
<td align="left"><p><strong>ConservativeScaling</strong>: RSS は、負荷を維持するために、できるだけ少ないプロセッサを使用します。 このオプションを使用すると、割り込みの回数を減らすことができます。</p></td>
</tr>
</tbody>
</table>

 

NDIS 6.30 では **\*RSSProfile**のサポートが追加されました。

次の一覧は、編集できる RSS の標準化された[INF キーワード](standardized-inf-keywords-for-network-devices.md)を示しています。

<a href="" id="---------rssbaseprocgroup"></a> **\*RssBaseProcGroup**  
**\*RssBaseProcNumber**キーワードに指定されているプロセッサ番号のプロセッサグループの番号。

<a href="" id="---------numanodeid"></a> **\*Num/Deid**  
ネットワークアダプターのメモリ割り当てに使用される優先 NUMA ノード。 また、オペレーティングシステムは、優先 NUMA ノードからの Cpu を最初に RSS に使用しようとします。

PCI 拡張カードのドライバーは、そのドライブが接続されている PCI スロットによって最も近いノードであるため、その INF で NUMA ノード ID を静的に指定しないでください。  ネットワークアダプターがシステムに統合されていて、NUMA ノードが事前に認識されていて、実行時に ACPI を照会することによってノードを判別できない場合は、 **\*numonly Deid**のみを指定します。

**注**  このキーワードが存在し、その値がコンピューター内の NUMA ノードの数より小さい場合、ndis では、 [**ndis\_RSS\_プロセッサ\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_rss_processor_info)構造体の**PreferredNumaNode**メンバーにこの値が使用されます。

 

**注**  Windows 8 では、NIC RSS プロファイルが**Numanodeid**(2) または**numascalingstatic**(3) に設定されている場合、 **\*numanodeid**値は無視されます。

 

<a href="" id="---------rssbaseprocnumber"></a> **\*RssBaseProcNumber**  
指定されたグループ内の基本 RSS プロセッサの番号。

<a href="" id="---------maxrssprocessors"></a> **\*MaxRssProcessors**  
RSS プロセッサの最大数。

<a href="" id="---------rssmaxprocnumber"></a> **\*RssMaxProcNumber**  
RSS インターフェイスのプロセッサの最大数。
**\*RssMaxProcNumber**を指定する場合は、 **\*RssMaxProcGroup**も指定する必要があります。

<a href="" id="---------rssmaxprocnumber"></a> **\*NumRSSQueues**  
RSS キューの数。

<a href="" id="---------rssmaxprocgroup"></a> **\*RssMaxProcGroup**RSS インターフェイスの最大プロセッサグループ。

**RssBaseProcGroup**と **\*RSSBASEPROCNUMBER**は、RSS で使用できる最小プロセッサ数を識別する PROCESSOR_NUMBER 構造体を形成します。\*
**RssMaxProcGroup**と **\*RSSMAXPROCNUMBER**は、RSS で使用できるプロセッサの最大数を識別する PROCESSOR_NUMBER 構造体を形成します。\*

たとえば、 **RssBaseProcGroup**が1に設定されていて、 **\*RssBaseProcNumber**が\*16 に設定されていて、 **RssMaxProcGroup**が3に設定されていて、 **\*RssMaxProcNumber**が8に設定されている場合\*とします。
<group>:<processor> 表記を使用した場合、基本プロセッサは1:16、最大プロセッサ数は3:8 です。
その後、プロセッサ0:0、0:32、1:0、および1:15 は、基本プロセッサ番号を下回るため、RSS の候補とは見なされません。
プロセッサ1:16、1:31、2:0、2:63、3:0、および3:8 はすべて RSS の候補と見なされます。これは、1:16 から3:8 までの範囲に含まれるためです。
プロセッサ3:9、3:31、および4:0 は、最大プロセッサ数を超えているため、RSS の候補とは見なされません。

NDIS 6.20 では、 **\*RssBaseProcGroup**、 **\*NumRssBaseProcNumber deid**、 **\*** 、および **\*MaxRssProcessors**キーワードのサポートが追加されました。

NDIS 6.30 では、 **\*RssMaxProcNumber**、 **\*NumRSSQueues**キーワードのサポートが追加されました。

編集可能な標準化された[INF キーワード](standardized-inf-keywords-for-network-devices.md)には、次の属性があります。

<a href="" id="subkeyname"></a>SubkeyName  
INF ファイルで指定する必要があり、レジストリに表示されるキーワードの名前。

<a href="" id="paramdesc"></a>ParamDesc  
SubkeyName に関連付けられている表示テキスト。

<a href="" id="type"></a>各種  
編集できる値の型。 値には、numeric (Int) または編集可能なテキスト (Edit) のいずれかを指定できます。

<a href="" id="default-value"></a>既定値  
整数またはテキストの既定値。 &lt;IHV が定義した&gt; は、その値が特定の独立系ハードウェアベンダー (IHV) の要件に関連付けられていることを示します。

<a href="" id="min"></a>」  
整数に使用できる最小値。 &lt;IHV が定義した&gt; は、最小値が特定の IHV 要件に関連付けられていることを示します。

<a href="" id="max"></a>制限  
整数に使用できる最大値。 &lt;IHV が定義した&gt; は、最小値が特定の IHV 要件に関連付けられていることを示します。

次の表では、編集できるすべての RSS キーワードについて説明します。

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
<th align="left">タスクバーの検索ボックスに</th>
<th align="left">既定値</th>
<th align="left">最小</th>
<th align="left">最大</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em>RssBaseProcGroup</strong></p></td>
<td align="left"><p>RSS 基本プロセッサグループ</p></td>
<td align="left"><p>整数</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>MAXIMUM_GROUPS-1</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em>Num/Deid</strong></p></td>
<td align="left"><p>優先 NUMA ノード</p></td>
<td align="left"><p>整数</p></td>
<td align="left"><p>65535 (任意のノード)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>システム固有-65534 を超えることはできません</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>RssBaseProcNumber</strong></p></td>
<td align="left"><p>RSS ベースプロセッサ番号</p></td>
<td align="left"><p>整数</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>MAXIMUM_PROC_PER_GROUP-1</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em>MaxRssProcessors</strong></p></td>
<td align="left"><p>RSS プロセッサの最大数</p></td>
<td align="left"><p>整数</p></td>
<td align="left"><p>Windows Server 2008 の既定値:</p>
<p>x 1G または低速のアダプターの場合は8、10G アダプターの場合は16</p>
<p>Windows 8 の既定値:</p>
<p>MSI-X がサポートされていない Nic については、1GbE または低速のアダプターの場合は4、10 GbE アダプターの場合は4です。</p>
<p>MSI-X のサポートが 1 Gbe または低速のアダプターの場合は4、10 GbE アダプターの場合は16。</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>MAXIMUM_PROC_PER_SYSTEM</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>RssMaxProcNumber</strong></p></td>
<td align="left"><p>RSS プロセッサの最大数</p></td>
<td align="left"><p>整数</p></td>
<td align="left"><p>MAXIMUM_PROC_PER_GROUP-1 (既定値)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>MAXIMUM_PROC_PER_GROUP-1</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em>NumRSSQueues</strong></p></td>
<td align="left"><p>RSS キューの最大数</p></td>
<td align="left"><p>整数</p></td>
<td align="left"><p>デバイス固有</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>デバイス固有</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>*RSSMaxProcGroup</strong></p></td>
<td align="left"><p>RSS 最大プロセッサグループ</p></td>
<td align="left"><p>整数</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>MAXIMUM_GROUPS-1</p></td>
</tr>
</tbody>
</table>

 

**注**   **\*RssBaseProcGroup**の有効な範囲は 0 ~\_グループ-1 で、Windows 7 では0である必要があります。 それ以外の場合、TCP/IP プロトコルは RSS にプロセッサを使用しません。

 

**注**   **\*Num/deid** (65535) の既定値は、ネットワークアダプターが NUMA ノードに依存しないことを意味し、NDIS は他のノードよりも優先されないようにします。
**\*NumaNodeId**キーワードが存在しない場合、NDIS は ACPI からのヒントに基づいて最も近いノードを自動的に選択します。


標準化された INF キーワードの詳細については、「[ネットワークデバイスの標準化](standardized-inf-keywords-for-network-devices.md)された inf キーワード」を参照してください。

 

 





