---
title: NDIS QoS 用の標準化された INF キーワード
description: NDIS QoS 用の標準化された INF キーワード
ms.assetid: 7967D633-850F-4707-9577-9262AEB1A597
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7909c3a62d8e3b647386c67a6b7b64932b45c5b7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841850"
---
# <a name="standardized-inf-keywords-for-ndis-qos"></a>NDIS QoS 用の標準化された INF キーワード


標準の INF キーワードは、ミニポートドライバーでの NDIS Quality of Service (QoS) のサポートを有効または無効にするために定義されています。

NDIS QoS をサポートするアダプターのミニポートドライバーの INF ファイルでは、 **\*QoS**の標準化された inf キーワードを指定する必要があります。 ドライバーがインストールされた後、管理者は、アダプターの **[詳細設定**] プロパティページで **\*QOS**キーワードの値を更新できます。 詳細プロパティの詳細については、「 [[詳細プロパティ] ページの構成パラメーターの指定](specifying-configuration-parameters-for-the-advanced-properties-page.md)」を参照してください。

アダプターの **[詳細設定**] プロパティページで変更が行われた後に、ミニポートドライバーが自動的に再起動  **ことに注意**してください。

 

**\*QOS** INF キーワードは列挙キーワードです。 次の表では、 **\*QOS** inf キーワードで使用できる inf エントリについて説明します。 この表の列では、列挙型キーワードの次の属性について説明します。

<a href="" id="subkeyname"></a>SubkeyName  
INF ファイルで指定する必要があるキーワードの名前。 この名前は、ネットワークアダプターの**Ndi\\params\\** キーの下のレジストリにも表示されます。

<a href="" id="paramdesc"></a>ParamDesc  
SubkeyName に関連付けられている表示テキスト。

独立系ハードウェアベンダー (IHV) では、SubkeyName の説明文を定義でき  ことに**注意**してください。

 

<a href="" id="value"></a>数値  
リスト内の各 SubkeyName に関連付けられている列挙整数値。

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
<td align="left"><p><strong>* QOS</strong></p></td>
<td align="left"><p>NDIS QoS</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>QoS 無効</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 (既定値)</p></td>
<td align="left"><p>QoS 有効</p></td>
</tr>
</tbody>
</table>

 

NDIS がミニポートドライバーの[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数を呼び出す場合、ドライバーは次の操作を行う必要があります。

-   ミニポートドライバーは、ネットワークアダプターがサポートする NDIS QoS ハードウェア機能を登録する必要があります。

-   また、ミニポートドライバーは、レジストリの **\*QOS**キーワード値を読み取って、アダプターの NDIS QOS ハードウェア機能の現在の状態を登録する必要があります。

ミニポートドライバーは、NDIS QoS ハードウェア機能の現在の状態を登録するときに、次のガイドラインに従う必要があります。

-   **\*QOS**キーワードの値が1の場合は、現在有効になっているすべての NDIS QOS ハードウェア機能をミニポートドライバーで登録する必要があります。 ドライバーは、次のことに関係なく、その NDIS QoS ハードウェア機能を有効にする必要があります。

    -   Microsoft Data Center ブリッジング (DCB) サーバー機能が Windows server 2012 以降のバージョンの Windows Server にインストールされているか、有効になっているか。 このサーバー機能と関連コンポーネントの詳細については、「[データセンターブリッジングの NDIS QoS アーキテクチャ](ndis-qos-architecture-for-data-center-bridging.md)」を参照してください。

    -   ローカルデータセンターブリッジング (DCBX) の状態がネットワークアダプターで有効になっているかどうか。 この状態が有効になっている場合、ネットワークアダプターとミニポートドライバーは、リモートピアから受信したリモート NDIS QoS パラメーターから動作している NDIS QoS パラメーターを解決できます。 詳細については、「[ローカル DCBX の状態の管理](managing-the-local-dcbx-willing-state.md)」を参照してください。

    QoS ハードウェアと現在の機能を登録する方法の詳細については、「 [NDIS Qos 機能の登録](registering-ndis-qos-capabilities.md)」を参照してください。

    ミニポートドライバーは、常に NDIS\_の状態を発行する必要が**あり  ** [ **\_qos\_操作\_パラメーター\_変更**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)と[**NDIS\_の状態\_QOS\_リモート\_のパラメーター\_** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-remote-parameters-change) 、その NDIS QoS ハードウェア機能が現在有効になっているかどうかを示します。 Windows Server 2012 以降では、これらの状態は、それぞれ現在の operational および remote QoS パラメーターの設定に関するレポートを示しています。 これらの表示により、システム管理者は、Microsoft DCB server 機能がインストールされているかどうかに関係なく、NDIS QoS および DCB 設定を表示できます。 詳細については、「 [NDIS QoS パラメーターの状態を示す](indicating-ndis-qos-parameter-status.md)」を参照してください。

     

-   **\*QOS**キーワードの値が0の場合は、現在無効になっているすべての NDIS QOS ハードウェア機能がミニポートドライバーによって報告される必要があります。 この場合、オペレーティングシステムは、NDIS QoS 機能を使用してドライバーを構成しません。

    **\*QOS**キーワードの値が0の場合は、DCB と dcbx をネットワークアダプターで無効にする必要があることに  **注意**してください。

     

-   **\*QOS**キーワードがレジストリに存在しない場合、ミニポートドライバーは、NDIS QOS ハードウェア機能を報告しないようにする必要があります。 この場合、オペレーティングシステムは、NDIS QoS 機能を使用してドライバーを構成しません。

    **\*QOS**キーワードがレジストリに存在しない場合は、ドライバー  ネットワークアダプターで DCB と dcbx を無効にする必要がある**ことに注意**してください。

     

**\*QOS**キーワードに加えて、ミニポートドライバーは、 **\*PriorityVLANTag**キーワードを読み取る必要があります。 このキーワードは、パケット優先順位および仮想 Lan (Vlan) の 802.1 Q タグを挿入するために、ネットワークアダプターを有効にするかどうかを指定します。

次の表は、 **\*QOS**と **\*PriorityVLANTag**キーワードの値の関係をまとめたものです。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">QOS キーワードの設定を <em></th>
<th align="left"></em>PriorityVLANTag キーワードの設定</th>
<th align="left">\* PriorityVLANTag 設定の説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">0または存在しない</td>
<td align="left"><p>0</p></td>
<td align="left"><p>VLAN 無効 & パケット優先順位</p></td>
</tr>
<tr class="even">
<td align="left">0または存在しない</td>
<td align="left"><p>1</p></td>
<td align="left"><p>パケットの優先順位の有効化</p></td>
</tr>
<tr class="odd">
<td align="left">0または存在しない</td>
<td align="left"><p>2</p></td>
<td align="left"><p>VLAN 有効</p></td>
</tr>
<tr class="even">
<td align="left">0または存在しない</td>
<td align="left"><p>3 (既定値)</p></td>
<td align="left"><p>パケットの優先順位と VLAN が有効</p></td>
</tr>
<tr class="odd">
<td align="left">1</td>
<td align="left"><p>0</p></td>
<td align="left"><p>パケットの優先順位の有効化</p></td>
</tr>
<tr class="even">
<td align="left">1</td>
<td align="left"><p>1</p></td>
<td align="left"><p>パケットの優先順位の有効化</p></td>
</tr>
<tr class="odd">
<td align="left">1</td>
<td align="left"><p>2</p></td>
<td align="left"><p>パケットの優先順位と VLAN が有効</p></td>
</tr>
<tr class="even">
<td align="left">1</td>
<td align="left"><p>3 (既定値)</p></td>
<td align="left"><p>パケットの優先順位と VLAN が有効</p></td>
</tr>
</tbody>
</table>

 

**\*PriorityVLANTag**キーワードの詳細については、「 [Enumeration Keywords](enumeration-keywords.md)」を参照してください。

標準化された INF キーワードの詳細については、「[ネットワークデバイスの標準化](standardized-inf-keywords-for-network-devices.md)された inf キーワード」を参照してください。

NDIS QoS 機能の登録方法の詳細については、「 [Ndis Qos 機能の登録](registering-ndis-qos-capabilities.md)」を参照してください。

 

 





