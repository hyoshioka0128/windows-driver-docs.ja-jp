---
title: SR-IOV 用の標準化された INF キーワード
description: SR-IOV 用の標準化された INF キーワード
ms.assetid: 5CA33B4F-E43A-4EB6-BCAB-365CA1FD3EF2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be4a693fb72929b0362e52769cff990a0cb95dd8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841842"
---
# <a name="standardized-inf-keywords-for-sr-iov"></a>SR-IOV 用の標準化された INF キーワード


このトピックでは、シングルルート i/o 仮想化 (SR-IOV) インターフェイスの標準化された INF キーワードについて説明します。 これらのキーワードは、SR-IOV ネットワークアダプターの PCI Express (PCIe) 物理機能 (PF) のミニポートドライバーの INF ファイルに適用されます。

SR-IOV INF キーワードについては、次のセクションで説明します。

[SR-IOV サポートを有効または無効にするための標準化された INF キーワード](#standardized-inf-keywords-for-enabling-or-disabling-sr-iov-support)

[既定の NIC スイッチを構成するための標準化された INF キーワード](#standardized-inf-keywords-for-configuration-of-the-default-nic-switch)

## <a name="standardized-inf-keywords-for-enabling-or-disabling-sr-iov-support"></a>SR-IOV サポートを有効または無効にするための標準化された INF キーワード


標準化された INF キーワードは、ネットワークアダプターの sr-iov 機能のサポートを有効または無効にするために定義されています。

<a href="" id="-sriov"></a> **\*SRIOV**  
デバイスで sr-iov 機能が有効または無効になっているかどうかを示す値。

ドライバーがインストールされた後、管理者は、ネットワークアダプターの **[詳細設定**] プロパティページで **\*SRIOV**キーワードの値を更新できます。 詳細プロパティの詳細については、「 [[詳細プロパティ] ページの構成パラメーターの指定](specifying-configuration-parameters-for-the-advanced-properties-page.md)」を参照してください。

アダプターの **[詳細設定**] プロパティページで変更が行われた後に、ミニポートドライバーが自動的に再起動  **ことに注意**してください。

 

<a href="" id="-sriovpreferred"></a> **\*Sriを優先**  
SR-IOV 機能を仮想マシンキュー (VMQ) または receive side scaling (RSS) 機能の代わりに有効にするかどうかを定義する値。

これは、INF ファイルで指定することができず、ネットワークアダプターの **[詳細設定**] プロパティページには表示されない、非表示のキーワード値です。

Sr-iov、VMQ、RSS のキーワードを解釈する方法の詳細については、「sr-iov、VMQ、RSS の標準化された[INF キーワードの処理](handling-sr-iov--vmq--and-rss-standardized-inf-keywords.md)」を参照してください。

SR-IOV の標準化された INF キーワードは列挙キーワードであり、次の表で説明します。 この表の列では、列挙型キーワードの次の属性について説明します。

<a href="" id="subkeyname"></a>SubkeyName  
INF ファイルで指定する必要があるキーワードの名前。 この名前は、ネットワークアダプターの**Ndi\\params\\** キーの下のレジストリにも表示されます。

<a href="" id="paramdesc"></a>ParamDesc  
**Subkeyname**キーワードに関連付けられている表示テキスト。

**注**   独立系ハードウェア ベンダー (IHV) は、SubkeyName のわかりやすいテキストを定義できます。

 

<a href="" id="value"></a>数値  
リスト内の各**Subkeyname**キーワードに関連付けられている列挙整数値。

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
<td align="left"><p><strong><em>SRIOV</strong></p></td>
<td align="left"><p>SR-IOV</p></td>
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
<td align="left"><p><strong></em>Sriを優先</strong></p></td>
<td align="left"><p>このサブキーの ParamDesc および EnumDesc エントリは、INF ファイルでもユーザーインターフェイスでも使用できません。</p></td>
<td align="left"><p>0 (既定値)</p></td>
<td align="left"><p><strong><em>VmqOrRssPreferrence</strong> キーワードに基づいて RSS または VMQ 機能を報告します。 Sr-iov 機能を報告しません。</p>
<p><strong></em>VmqOrRssPreferrence</strong>キーワードの詳細については、「 <a href="standardized-inf-keywords-for-vmq.md" data-raw-source="[Standardized INF Keywords for VMQ](standardized-inf-keywords-for-vmq.md)">VMQ の標準化</a>された INF キーワード」を参照してください。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>Sr-iov 機能を報告します。</p></td>
</tr>
</tbody>
</table>

 

標準化された INF キーワードの詳細については、「[ネットワークデバイスの標準化](standardized-inf-keywords-for-network-devices.md)された inf キーワード」を参照してください。

## <a name="standardized-inf-keywords-for-configuration-of-the-default-nic-switch"></a>既定の NIC スイッチを構成するための標準化された INF キーワード


Windows Server 2012 以降では、SR-IOV インターフェイスはネットワークアダプター上で1つの NIC スイッチのみをサポートしています。 このスイッチは*既定の NIC スイッチ*と呼ばれ、NDIS\_既定\_スイッチ\_ID 識別子によって参照されます。

PF ミニポートドライバーの INF ファイルでは、sr-iov ネットワークアダプターの既定の NIC スイッチの構成を指定する必要があります。 これにより、ネットワークインストーラーは、既定のスイッチ構成情報を INF から既定のスイッチのサブキーの下のミニポートレジストリ構成にコピーできるようになります (**Ndi\\params\\NicSwitches\\0**)。

これらのキーワードは、ネットワークアダプターの **[詳細設定**] プロパティページには表示されず、ユーザーが構成することはできません。 これらのキーワードは、INF ファイルの**Ddinstall**セクションの**AddReg**ディレクティブを使用して指定します。 各キーワードは、個別の**AddReg**ディレクティブによって指定されます。

次の表では、SR-IOV ネットワークアダプターの既定の NIC スイッチ構成に関する INF キーワードについて説明します。 この表の列では、これらのキーワードの次の属性について説明します。

<a href="" id="subkeyname"></a>SubkeyName  
INF ファイルで指定する必要があるキーワードの名前。 この名前は、ネットワークアダプターの**Ndi\\params\\NicSwitches\\0**キーの下のレジストリにも表示されます。

<a href="" id="data-value"></a>データ値  
**Subkeyname**キーワードに関連付けられている値。

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
<th align="left">データの種類</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em>フラグ</strong></p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>REG_DWORD</p></td>
<td align="left"><p>キーワードには、この値を代入する必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em>SwitchType</strong></p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>REG_DWORD</p></td>
<td align="left"><p>キーワードには、この値を代入する必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>SwitchId</strong></p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>REG_DWORD</p></td>
<td align="left"><p>キーワードには、この値を代入する必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em>SwitchName</strong></p></td>
<td align="left"><p>"既定のスイッチ"</p></td>
<td align="left"><p>REG_SZ</p></td>
<td align="left"><p>キーワードには、この値を代入する必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>* NumVFs</strong></p></td>
<td align="left"><p>(0 ~<em>n</em>)、</p></td>
<td align="left"><p>REG_DWORD</p></td>
<td align="left"><p><em>n</em>は、sr-iov ネットワークアダプターによってサポートされる PCIe 仮想関数 (VFs) の最大数です。</p>
<div class="alert">
<strong>メモ</strong> このレジストリキーは、ネットワークアダプターがサポートする VFs の最大数を定義します。 ミニポートドライバーは<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes" data-raw-source="[&lt;strong&gt;NdisMSetMiniportAttributes&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)"><strong>NdisMSetMiniportAttributes</strong></a>を呼び出すと、ネットワークアダプターの使用可能なハードウェアリソースに応じて、この値よりも少ないアドバタイズを行うことができます。 詳細については、「 <a href="determining-nic-switch-capabilities.md" data-raw-source="[Determining NIC Switch Capabilities](determining-nic-switch-capabilities.md)">NIC スイッチの機能の確認</a>」を参照してください。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

SR-IOV ネットワークアダプターの既定の NIC スイッチ構成の**AddReg**ディレクティブの例を次に示します。

``` syntax
HKR, NicSwitches\0, *SwitchId,   0x00010001, 0
HKR, NicSwitches\0, *SwitchName, 0x00000000, “Default Switch”
```

**AddReg**ディレクティブの構文の詳細については、「 [**INF AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)」を参照してください。

既定の NIC スイッチの詳細については、「 [Nic スイッチ](nic-switches.md)」を参照してください。

 

 





