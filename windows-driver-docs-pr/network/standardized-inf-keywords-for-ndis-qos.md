---
title: NDIS QoS 用の標準化された INF キーワード
description: NDIS QoS 用の標準化された INF キーワード
ms.assetid: 7967D633-850F-4707-9577-9262AEB1A597
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 236ea7fa353a460c774fc4786b96903d84289291
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345980"
---
# <a name="standardized-inf-keywords-for-ndis-qos"></a>NDIS QoS 用の標準化された INF キーワード


有効またはミニポート ドライバーで NDIS サービスの品質 (QoS) のサポートを無効にするには、標準化された INF キーワードが定義されます。

NDIS QoS をサポートするアダプターのミニポート ドライバーの INF ファイルを指定する必要があります、  **\*QOS** INF キーワードを標準化します。 ドライバーがインストールされている場合後の管理者を更新できます、  **\*QOS**でキーワード値、 **[詳細設定]** アダプターのプロパティ ページ。 高度なプロパティの詳細については、次を参照してください。[プロパティの詳細 ページの構成パラメーターを指定する](specifying-configuration-parameters-for-the-advanced-properties-page.md)します。

**注**  ミニポート ドライバーが自動的に再起動で、変更を行った後、 **[詳細設定]** アダプターのプロパティ ページ。

 

 **\*QOS** INF キーワードは、キーワードを列挙します。 次の表に、考えられる INF エントリ、  **\*QOS** INF キーワード。 このテーブルの列には、列挙型のキーワードは次の属性について説明します。

<a href="" id="subkeyname"></a>SubkeyName  
INF ファイルで指定する必要があります、キーワードの名前。 この名前は、下のレジストリにも表示されます、 **NDI\\params\\** ネットワーク アダプターのキー。

<a href="" id="paramdesc"></a>ParamDesc  
SubkeyName に関連付けられているテキスト。

**注**  SubkeyName の独立系ハードウェア ベンダー (IHV) が、わかりやすいテキストを定義できます。

 

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
<th align="left">[値]</th>
<th align="left">EnumDesc</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>* QOS</strong></p></td>
<td align="left"><p>NDIS QoS</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>QoS を無効になっています</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 (既定)</p></td>
<td align="left"><p>QoS を有効になっています。</p></td>
</tr>
</tbody>
</table>

 

NDIS のミニポート ドライバーの呼び出したときに[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数の場合、ドライバーは、次を実行する必要があります。

-   ミニポート ドライバーでは、ネットワーク アダプターをサポートする NDIS QoS ハードウェア機能を登録する必要があります。

-   ミニポート ドライバーを参照する必要がありますも、  **\*QOS**アダプターの NDIS QoS ハードウェア機能の現在の状態を登録するレジストリのキーワード値。

NDIS QoS のハードウェア機能の現在の状態を登録するとき、ミニポート ドライバーは次のガイドラインに従う必要があります。

-   場合、  **\*QOS**キーワードは、1 つの値を持つ、ミニポート ドライバーでは、現在有効になっているすべての NDIS QoS ハードウェア機能を登録する必要があります。 ドライバーに関係なく、次の NDIS QoS のハードウェア機能が有効にする必要があります。

    -   Microsoft データ センター ブリッジング (DCB) サーバーの機能がインストールまたは Windows Server 2012 およびそれ以降のバージョンの Windows Server で有効になっているかどうか。 このサーバーの機能と関連コンポーネントの詳細については、次を参照してください。[データ センター ブリッジングの NDIS QoS アーキテクチャ](ndis-qos-architecture-for-data-center-bridging.md)します。

    -   ネットワーク アダプターで、ローカル Data Center Bridging Exchange (DCBX) しようとして状態を有効かどうか。 この状態が有効にすると、ネットワーク アダプターとミニポート ドライバーはリモート ピアから受信したリモートの NDIS QoS パラメーターから、運用の NDIS QoS パラメーターを解決できます。 詳細については、次を参照してください。 [DCBX 許容状態のローカル管理](managing-the-local-dcbx-willing-state.md)します。

    QoS のハードウェアと現在の機能を登録する方法の詳細については、次を参照してください。 [NDIS QoS 機能の登録](registering-ndis-qos-capabilities.md)します。

    **注**  ミニポート ドライバーが常に発行する必要があります[ **NDIS\_状態\_QOS\_運用\_パラメーター\_変更**](https://msdn.microsoft.com/library/windows/hardware/hh439810)と[ **NDIS\_状態\_QOS\_リモート\_パラメーター\_変更**](https://msdn.microsoft.com/library/windows/hardware/hh439812)状態NDIS QoS ハードウェア機能が現在有効になっている場合に表示します。 Windows Server 2012、現在の運用上およびリモート QoS パラメーター設定に、これらの状態がないレポートでそれぞれ開始しています。 これらの問題では、NDIS QoS と DCB の Microsoft サーバーの機能がインストールされているかどうかに関係なく DCB 設定を表示するシステム管理者を使用できます。 詳細については、次を参照してください。 [NDIS QoS パラメーターの状態のことを示す](indicating-ndis-qos-parameter-status.md)します。

     

-   場合、  **\*QOS**キーワードが 0 の値を持つ、ミニポート ドライバーでは、現在無効になっているすべての NDIS QoS ハードウェア機能を報告する必要があります。 ここでは、オペレーティング システムでは、NDIS QoS 機能を備えた、ドライバーが構成はしません。

    **注**  ドライバーおよび無効にする DCB DCBX ネットワーク アダプターの場合、  **\*QOS**キーワードには、ゼロの値。

     

-   場合、  **\*QOS**キーワードがレジストリに存在しない、ミニポート ドライバーが任意の NDIS QoS ハードウェア機能を報告する必要があります。 ここでは、オペレーティング システムでは、NDIS QoS 機能を備えた、ドライバーが構成はしません。

    **注**  ドライバーおよび無効にする DCB DCBX ネットワーク アダプターの場合、  **\*QOS**キーワードは、レジストリに存在しません。

     

加え、  **\*QOS**キーワード、ミニポート ドライバーが読み取る必要があります、  **\*PriorityVLANTag**キーワード。 このキーワードは、802.1 q を挿入するネットワーク アダプターが有効になっているかどうかを指定します。 パケットの優先順位と仮想 Lan (Vlan) のタグ。

次の表に、間のリレーションシップ、  **\*QOS**と **\*PriorityVLANTag**キーワードの値。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><em>QOS キーワードの設定</th>
<th align="left"></em>PriorityVLANTag キーワードの設定</th>
<th align="left">* PriorityVLANTag 設定の説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">0 または存在しません。</td>
<td align="left"><p>0</p></td>
<td align="left"><p>パケットの優先順位&amp;VLAN 無効</p></td>
</tr>
<tr class="even">
<td align="left">0 または存在しません。</td>
<td align="left"><p>1</p></td>
<td align="left"><p>パケットの優先順位が有効になっています。</p></td>
</tr>
<tr class="odd">
<td align="left">0 または存在しません。</td>
<td align="left"><p>2</p></td>
<td align="left"><p>VLAN 有効</p></td>
</tr>
<tr class="even">
<td align="left">0 または存在しません。</td>
<td align="left"><p>3 (既定値)</p></td>
<td align="left"><p>パケットの優先順位と VLAN を有効になっています。</p></td>
</tr>
<tr class="odd">
<td align="left">1</td>
<td align="left"><p>0</p></td>
<td align="left"><p>パケットの優先順位が有効になっています。</p></td>
</tr>
<tr class="even">
<td align="left">1</td>
<td align="left"><p>1</p></td>
<td align="left"><p>パケットの優先順位が有効になっています。</p></td>
</tr>
<tr class="odd">
<td align="left">1</td>
<td align="left"><p>2</p></td>
<td align="left"><p>パケットの優先順位と VLAN を有効になっています。</p></td>
</tr>
<tr class="even">
<td align="left">1</td>
<td align="left"><p>3 (既定値)</p></td>
<td align="left"><p>パケットの優先順位と VLAN を有効になっています。</p></td>
</tr>
</tbody>
</table>

 

詳細については、  **\*PriorityVLANTag**キーワードを参照してください[列挙キーワード](enumeration-keywords.md)します。

標準化された INF キーワードの詳細については、次を参照してください。[ネットワーク デバイスの標準化された INF キーワード](standardized-inf-keywords-for-network-devices.md)します。

NDIS QoS 機能を登録する方法の詳細については、次を参照してください。 [NDIS QoS 機能の登録](registering-ndis-qos-capabilities.md)します。

 

 





