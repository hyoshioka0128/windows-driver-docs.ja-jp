---
title: SR-IOV、VMQ、および RSS の標準化された INF キーワードの処理
description: SR-IOV、VMQ、および RSS の標準化された INF キーワードの処理
ms.assetid: EF556563-4097-4388-A563-29FC891AC626
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76e0dfe1be079ae85d9ffb1ea478799e2b22bbf2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842562"
---
# <a name="handling-sr-iov-vmq-and-rss-standardized-inf-keywords"></a>SR-IOV、VMQ、および RSS の標準化された INF キーワードの処理


シングルルート i/o 仮想化 (SR-IOV)、仮想マシンキュー (VMQ)、receive side scaling (RSS) をサポートするネットワークアダプターでは、次の方法でこれらのインターフェイスを使用できます。

-   Sr-iov と VMQ は、個別に、または同時に有効にすることができます。

-   SR-IOV または VMQ が有効になっている場合、ネットワークアダプターで RSS を有効にすることはできません。

オペレーティングシステムにより、sr-iov、VMQ、または RSS インターフェイスを次のように使用できるようになります。

-   ネットワークアダプターが TCP/IP スタックにバインドされている場合、この動作により RSS 機能を使用できるようになります。

-   ネットワークアダプターが Hyper-v 拡張可能スイッチドライバースタックにバインドされている場合、オペレーティングシステムは sr-iov または VMQ 機能のいずれかを使用できます。

    Hyper-v 拡張可能スイッチの詳細については、「 [Hyper-v 拡張可能スイッチ](hyper-v-extensible-switch.md)」を参照してください。

ネットワークアダプターが TCP/IP スタックと Hyper-v 拡張可能スイッチドライバースタックからバインド解除されると、ミニポートドライバーが停止してから再初期化されます。 このため、このようなネットワークアダプターは RSS、VMQ、および sr-iov を自動的に切り替えることはできません。

NDIS が[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数を呼び出すと、ミニポートドライバーは、現在有効になっている SR-IOV、VMQ、RSS の各機能を ndis に報告する前に、次の手順に従います。

1.  ミニポートドライバーは、現在有効になっている機能を NDIS に報告する前に、 **\*Sriの優先**キーワードを読み取ります。

    **Sri\*優先**キーワードの値が1の場合、ミニポートドライバーは sr-iov 設定用に構成されています。

2.  ミニポートドライバーは、現在有効になっている機能を NDIS に報告する前に、 **\*RssOrVmqPreference**キーワードを読み取ります。

    **\*RssOrVmqPreference**キーワードの値が1の場合、ミニポートドライバーは VMQ 優先順位用に構成されています。

    **\*RssOrVmqPreference**キーワードの値が0であるか、キーワードが存在しない場合、ミニポートドライバーは RSS 設定用に構成されます。

3.  ミニポートドライバーが sr-iov 設定用に構成されている場合は、ネットワークアダプターで sr-iov が有効になっているかどうかを確認するために、 **\*SRIOV**キーワードを読み取る必要があります。 キーワードが1に設定されている場合は、現在有効になっている SR-IOV 設定がドライバーによって報告されます。

    ミニポートドライバーが sr-iov 設定を報告する方法の詳細については、「sr-iov[機能の決定](determining-sr-iov-capabilities.md)」を参照してください。

    Sr-iov キーワードの詳細については、「sr-iov[用の標準化](standardized-inf-keywords-for-sr-iov.md)された INF キーワード」を参照してください。

    **注**  sr-iov の設定用にミニポートドライバーが構成されている場合は、RSS の標準化されたキーワードを読み取ることができません。 ただし、ドライバーは VMQ **\*VMQVlanFiltering**標準化されたキーワードを読み取る必要があります。 このキーワードは、ミニポートドライバーが、メディアアクセスコントロール (MAC) ヘッダーの仮想 VLAN (VLAN) 識別子を使用してネットワークパケットをフィルター処理できるようにするかどうかを指定します。 ミニポートドライバーは、ndis\_受信\_フィルター\_MAC\_ヘッダー\_VLAN\_ID\_Ndis の**SupportedMacHeaderFields**メンバーでサポートされているフラグを設定することによって、この機能を報告し[ **\_受信\_フィルター\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)の構造です。 **\*VMQVlanFiltering**の標準化されたキーワードの詳細については、「 [VMQ の標準化](standardized-inf-keywords-for-vmq.md)された INF キーワード」を参照してください。

     

4.  ミニポートドライバーが VMQ 優先用に構成されている場合、ネットワークアダプターで VMQ が有効になっているかどうかを確認するには、 **\*vmq**キーワードを読み取る必要があります。 キーワードが1に設定されている場合は、現在有効になっている VMQ の設定がドライバーによって報告されます。 ミニポートドライバーが VMQ 設定を報告する方法の詳細については、「[ネットワークアダプターの Vmq 機能の決定](determining-the-vmq-capabilities-of-a-network-adapter.md)」を参照してください。

    VMQ キーワードの詳細については、「 [vmq の標準化](standardized-inf-keywords-for-vmq.md)された INF キーワード」を参照してください。

    **注**  ミニポートドライバーが VMQ に設定されている場合は、RSS または sr-iov の標準化されたキーワードを読み取ることができません。

     

5.  ミニポートドライバーが RSS 設定用に構成されている場合、ネットワークアダプターで RSS が有効になっているかどうかを確認するには、 **\*の rss**キーワードを読む必要があります。 キーワードが1に設定されている場合は、現在有効になっている RSS 設定がドライバーによって報告されます。 ミニポートドライバーが RSS 設定を報告する方法の詳細については、「 [rss の構成](rss-configuration.md)」を参照してください。

    RSS キーワードの詳細については、「 [rss 用の標準化](standardized-inf-keywords-for-rss.md)された INF キーワード」を参照してください。

    **注**  ミニポートドライバーが RSS 設定用に構成されている場合は、VMQ または sr-iov の標準化されたキーワードを読み取ることができません。

     

次の表は、ネットワークアダプターで正しいインターフェイスを有効にするために、ミニポートドライバーによって sr-iov、VMQ、または RSS の設定がどのように決定されるかを示しています。

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
<th align="left"><em>Sriを優先</th>
<th align="left"></em>RssOrVmqPreference</th>
<th align="left"><em>SRIOV</th>
<th align="left"></em>VMQ</th>
<th align="left">\* RSS</th>
<th align="left">有効なインターフェイス</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>該当なし</p></td>
<td align="left"><p>Sr-iov と VMQ</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>該当なし</p></td>
<td align="left"><p>VMQ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>1、0、またはレジストリに存在しません。</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>該当なし</p></td>
<td align="left"><p>なし</p></td>
</tr>
<tr class="even">
<td align="left"><p>0、またはレジストリに存在しません。</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>該当なし</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>該当なし</p></td>
<td align="left"><p>VMQ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0、またはレジストリに存在しません。</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>該当なし</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>該当なし</p></td>
<td align="left"><p>なし</p></td>
</tr>
<tr class="even">
<td align="left"><p>0、またはレジストリに存在しません。</p></td>
<td align="left"><p>0、またはレジストリに存在しません。</p></td>
<td align="left"><p>該当なし</p></td>
<td align="left"><p>該当なし</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>RSS</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0、またはレジストリに存在しません。</p></td>
<td align="left"><p>0、またはレジストリに存在しません。</p></td>
<td align="left"><p>該当なし</p></td>
<td align="left"><p>該当なし</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>なし</p></td>
</tr>
</tbody>
</table>

 

**注**  SR-IOV と vmq のインターフェイスの両方が有効になっている場合、PCI Express (PCIe) 物理機能 (PF) に接続されている sr-iov の既定以外の仮想ポート (vports) は、VMQ インターフェイスの VM キューの代わりに使用されます。 詳細については、「[既定以外の仮想ポートと VMQ](nondefault-virtual-ports-and-vmq.md)」を参照してください。

 

ミニポートドライバーは、現在有効になっているインターフェイスの機能をアドバタイズする必要があります。 たとえば、sr-iov が有効になっている場合、ミニポートドライバーは sr-iov 機能をアドバタイズする必要がありますが、VMQ または RSS の機能は提供しません。 ただし、ミニポートドライバーは、ネットワークアダプターで有効になっているインターフェイスに関係なく、RSS、VMQ、および SR-IOV の完全なハードウェア機能を常に報告する必要があります。

VMQ および sr-iov インターフェイスは、VM キューまたは sr-iov 仮想ポート (VPorts) に対して受信フィルター処理を使用する  に**注意**してください。 そのため、これらのインターフェイスのいずれかが有効になっている場合、一部の受信フィルター処理機能には同じまたは異なる設定が必要です。 SR-IOV インターフェイスの受信フィルター処理機能を報告する方法の詳細については、「[受信フィルター機能の決定](determining-receive-filtering-capabilities.md)」を参照してください。 VMQ インターフェイスの受信フィルター処理機能を報告する方法の詳細については、「[ネットワークアダプターの Vmq 機能の決定](determining-the-vmq-capabilities-of-a-network-adapter.md)」を参照してください。

 

 

 





