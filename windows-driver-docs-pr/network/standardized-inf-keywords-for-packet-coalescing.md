---
title: パケットの結合の標準化された INF キーワード
description: パケットの結合の標準化された INF キーワード
ms.assetid: 423E9B50-6474-454A-97BB-91404DF9F729
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76402d713dcde5ea18730920425a1e5b45574c70
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529654"
---
# <a name="standardized-inf-keywords-for-packet-coalescing"></a>パケットの結合の標準化された INF キーワード


有効またはパケットの結合、ミニポート ドライバーでのサポートを無効にするには、標準化された INF キーワードが定義されます。

パケットの結合をサポートするアダプターのミニポート ドライバーの INF ファイルを指定する必要があります、  **\*PacketCoalescing** INF キーワードを標準化します。 ドライバーがインストールされると、管理者を更新できる、  **\*PacketCoalescing**でキーワード値、 **[詳細設定]** アダプターのプロパティ ページ。 高度なプロパティの詳細については、次を参照してください。[プロパティの詳細 ページの構成パラメーターを指定する](specifying-configuration-parameters-for-the-advanced-properties-page.md)します。

**注**  ミニポート ドライバーが自動的に再起動で、変更を行った後、 **[詳細設定]** アダプターのプロパティ ページ。

 

 **\*PacketCoalescing** INF キーワードは、キーワードを列挙します。 次の表に、考えられる INF エントリ、  **\*PacketCoalescing** INF キーワード。 このテーブルの列には、列挙型のキーワードは次の属性について説明します。

<a href="" id="subkeyname"></a>SubkeyName  
INF ファイルで指定する必要があります、キーワードの名前。 この名前は、下のレジストリにも表示されます、 **NDI\\params\\** ネットワーク アダプターのキー。

<a href="" id="paramdesc"></a>ParamDesc  
SubkeyName に関連付けられているテキスト。

**注**  独立系ハードウェア ベンダー (IHV) は、SubkeyName のわかりやすいテキストを定義できます。

 

<a href="" id="value"></a>値  
一覧で各 SubkeyName に関連付けられている列挙型の整数値。

<a href="" id="enumdesc"></a>EnumDesc  
メニューに表示される各値に関連付けられている表示テキスト。

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
<td align="left"><p><strong>*PacketCoalescing</strong></p></td>
<td align="left"><p>パケットの結合</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>無効</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 (既定)</p></td>
<td align="left"><p>有効</p></td>
</tr>
</tbody>
</table>

 

ミニポート ドライバーを確認する必要があります、  **\*PacketCoalescing**パケットの結合のサポートをアドバタイズする前に、レジストリ内のキーワード値。 場合、  **\*PacketCoalescing**キーワードが 0 の値を持つ、ミニポートは、パケットの結合機能のサポートをアドバタイズする必要があります。 詳細については、次を参照してください。[パケット結合機能の報告](reporting-packet-coalescing-capabilities.md)します。

標準化された INF キーワードの詳細については、次を参照してください。[ネットワーク デバイスの標準化された INF キーワード](standardized-inf-keywords-for-network-devices.md)します。

 

 





