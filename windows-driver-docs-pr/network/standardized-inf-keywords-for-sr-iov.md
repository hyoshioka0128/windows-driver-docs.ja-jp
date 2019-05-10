---
title: SR-IOV 用の標準化された INF キーワード
description: SR-IOV 用の標準化された INF キーワード
ms.assetid: 5CA33B4F-E43A-4EB6-BCAB-365CA1FD3EF2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d672152a3d05be03d22b4bee5635aa24a6dfacb
ms.sourcegitcommit: 0504cc497918ebb7b41a205f352046a66c0e26a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2019
ms.locfileid: "65405275"
---
# <a name="standardized-inf-keywords-for-sr-iov"></a>SR-IOV 用の標準化された INF キーワード


このトピックでは、シングル ルート I/O 仮想化 (SR-IOV) インターフェイスの標準化された INF キーワードについて説明します。 これらのキーワードは、、PCI Express (PCIe) 物理機能 (PF)、SR-IOV ネットワーク アダプターのミニポート ドライバーの INF ファイルに適用されます。

SR-IOV INF キーワードは、次のセクションで説明します。

[有効または無効の SR-IOV サポートするための標準化された INF キーワード](#standardized-inf-keywords-for-enabling-or-disabling-sr-iov-support)

[既定の NIC のスイッチの構成の標準化された INF キーワード](#standardized-inf-keywords-for-configuration-of-the-default-nic-switch)

## <a name="standardized-inf-keywords-for-enabling-or-disabling-sr-iov-support"></a>有効にする、または SR-IOV サポートを無効にするための標準化された INF キーワード


有効にするか、ネットワーク アダプターの SR-IOV 機能のサポートを無効にするのには、標準化された INF キーワードが定義されています。

<a href="" id="-sriov"></a>**\*SRIOV**  
デバイスが有効になっているまたは SR-IOV 機能を無効になっているかどうかを示す値。

管理者を更新できます、ドライバーがインストールされた後、  **\*SRIOV**でキーワード値、 **[詳細設定]** ネットワーク アダプターのプロパティ ページ。 高度なプロパティの詳細については、次を参照してください。[プロパティの詳細 ページの構成パラメーターを指定する](specifying-configuration-parameters-for-the-advanced-properties-page.md)します。

**注**  ミニポート ドライバーが自動的に再起動で、変更を行った後、 **[詳細設定]** アダプターのプロパティ ページ。

 

<a href="" id="-sriovpreferred"></a>**\*SriovPreferred**  
SR-IOV 機能が仮想マシン キュー (VMQ) の代わりに有効にする必要がありますまたは受信側のスケーリング (RSS) の機能かどうかを定義する値。

これは、INF ファイルで指定する必要がありますいないに表示されていない非表示のキーワード値**詳細**ネットワーク アダプターのプロパティ ページ。

SR-IOV、VMQ、および RSS キーワードの解釈方法の詳細については、次を参照してください。[処理、SR-IOV、VMQ、および RSS の標準化された INF キーワード](handling-sr-iov--vmq--and-rss-standardized-inf-keywords.md)します。

SR-IOV 標準化された INF キーワード列挙型のキーワードし、は、次の表で説明します。 このテーブルの列には、列挙型のキーワードは次の属性について説明します。

<a href="" id="subkeyname"></a>SubkeyName  
INF ファイルで指定する必要があります、キーワードの名前。 この名前は、下のレジストリにも表示されます、 **NDI\\params\\** ネットワーク アダプターのキー。

<a href="" id="paramdesc"></a>ParamDesc  
関連付けられている表示テキスト、**SubkeyName**キーワード。

**注**  独立系ハードウェア ベンダー (IHV) は、SubkeyName のわかりやすいテキストを定義できます。

 

<a href="" id="value"></a>値  
列挙体の整数値に関連付けられた各**SubkeyName**キーワードをリストにします。

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
<td align="left"><p><strong><em>SRIOV</strong></p></td>
<td align="left"><p>SR-IOV</p></td>
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
<td align="left"><p><strong></em>SriovPreferred</strong></p></td>
<td align="left"><p>このサブキーの ParamDesc と EnumDesc のエントリは、INF ファイルやユーザー インターフェイスのいずれかで使用できません。</p></td>
<td align="left"><p>0 (既定)</p></td>
<td align="left"><p>に基づいて RSS または VMQ 機能の報告、 <strong> <em>VmqOrRssPreferrence</strong>キーワード。 SR-IOV 対応の機能を報告しません。</p>
<p>詳細については、  <strong></em>VmqOrRssPreferrence</strong>キーワードを参照してください<a href="standardized-inf-keywords-for-vmq.md" data-raw-source="[Standardized INF Keywords for VMQ](standardized-inf-keywords-for-vmq.md)">VMQ の標準化された INF キーワード</a>します。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>SR-IOV 機能をレポートします。</p></td>
</tr>
</tbody>
</table>

 

標準化された INF キーワードの詳細については、次を参照してください。[ネットワーク デバイスの標準化された INF キーワード](standardized-inf-keywords-for-network-devices.md)します。

## <a name="standardized-inf-keywords-for-configuration-of-the-default-nic-switch"></a>既定の NIC のスイッチの構成の標準化された INF キーワード


Windows Server 2012 以降では、SR-IOV インターフェイス NIC スイッチが 1 つだけをサポート、ネットワーク アダプターします。 このスイッチと呼ばれる、 *NIC スイッチの既定*、NDIS によって参照されている\_既定\_スイッチ\_ID です。

PF ミニポート ドライバーの INF ファイルは、SR-IOV ネットワーク アダプターの NIC スイッチの既定の構成を指定する必要があります。 これにより、INF からミニポート レジストリ構成を既定のスイッチのサブキーの下に既定のスイッチの構成情報をコピーするネットワーク インストーラー (**NDI\\params\\NicSwitches\\0**)。

これらのキーワードは表示されません、**詳細**プロパティは、ネットワーク アダプターのページし、ユーザーが構成することはできません。 使用してこれらのキーワードが指定されて、 **AddReg**ディレクティブで、 **DDInstall** INF ファイルのセクション。 それぞれのキーワードが個別で指定された**AddReg**ディレクティブ。

次の表では、SR-IOV ネットワーク アダプターの既定の NIC スイッチ構成 INF キーワードについて説明します。 このテーブルの列には、これらのキーワードは次の属性について説明します。

<a href="" id="subkeyname"></a>SubkeyName  
INF ファイルで指定する必要があります、キーワードの名前。 この名前は、下のレジストリにも表示されます、 **NDI\\params\\NicSwitches\\0**ネットワーク アダプターのキー。

<a href="" id="data-value"></a>データ値  
関連付けられている値、 **SubkeyName**キーワード。

<a href="" id="data-type"></a>データ型  
データ値の型。

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
<th align="left">データ値</th>
<th align="left">データ型</th>
<th align="left">メモ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em>フラグ</strong></p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>REG_DWORD</p></td>
<td align="left"><p>キーワードには、この値を割り当てる必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em>SwitchType</strong></p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>REG_DWORD</p></td>
<td align="left"><p>キーワードには、この値を割り当てる必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>SwitchId</strong></p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>REG_DWORD</p></td>
<td align="left"><p>キーワードには、この値を割り当てる必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em>SwitchName</strong></p></td>
<td align="left"><p>「既定のスイッチ」</p></td>
<td align="left"><p>REG_SZ</p></td>
<td align="left"><p>キーワードには、この値を割り当てる必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>* NumVFs</strong></p></td>
<td align="left"><p>(0 -<em>n</em>)、</p></td>
<td align="left"><p>REG_DWORD</p></td>
<td align="left"><p><em>n</em>の PCIe 仮想機能 (Vf)、SR-IOV ネットワーク アダプターでサポートされている最大数です。</p>
<div class="alert">
<strong>注</strong>このレジストリ キーは、ネットワーク アダプターをサポートするための VFs の最大数を定義します。 ミニポート ドライバーを呼び出すと<a href="https://msdn.microsoft.com/library/windows/hardware/ff563672" data-raw-source="[&lt;strong&gt;NdisMSetMiniportAttributes&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563672)"> <strong>NdisMSetMiniportAttributes</strong></a>、ネットワーク アダプターで使用可能なハードウェア リソースによっては、この値より小さい、アドバタイズできます。 詳細については、次を参照してください。 <a href="determining-nic-switch-capabilities.md" data-raw-source="[Determining NIC Switch Capabilities](determining-nic-switch-capabilities.md)">NIC スイッチの機能を決定する</a>します。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

次の例に示します**AddReg**ディレクティブ、SR-IOV ネットワーク アダプターの既定の NIC スイッチ構成。

``` syntax
HKR, NicSwitches\0, *SwitchId,   0x00010001, 0
HKR, NicSwitches\0, *SwitchName, 0x00000000, “Default Switch”
```

構文の詳細については、 **AddReg**ディレクティブを参照してください[ **INF AddReg ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546320)します。

既定の NIC のスイッチの詳細については、次を参照してください。 [NIC スイッチ](nic-switches.md)します。

 

 





