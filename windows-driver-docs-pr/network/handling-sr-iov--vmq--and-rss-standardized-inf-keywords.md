---
title: SR-IOV、VMQ、および RSS の標準化された INF キーワードの処理
description: SR-IOV、VMQ、および RSS の標準化された INF キーワードの処理
ms.assetid: EF556563-4097-4388-A563-29FC891AC626
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 091d8b2fda2829dc24af30d0c6330e4ffb8b1d61
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381357"
---
# <a name="handling-sr-iov-vmq-and-rss-standardized-inf-keywords"></a>SR-IOV、VMQ、および RSS の標準化された INF キーワードの処理


シングル ルート I/O 仮想化 (SR-IOV) 仮想マシン キュー (VMQ) をサポートし、受信側 scaling (RSS) ネットワーク アダプターは、次のように、これらのインターフェイスの使用を有効にできます。

-   個別にまたは同時に、SR-IOV と VMQ を有効にすることができます。

-   SR-IOV または VMQ が有効にすると、ネットワーク アダプターで RSS を有効にできません。

オペレーティング システムでは、次のように、SR-IOV、VMQ、または RSS インターフェイスの使用を有効にします。

-   TCP/IP スタックにネットワーク アダプターがバインドされると、オペレーティング システムは、RSS 機能を使用できるようにします。

-   ネットワーク アダプターが HYPER-V 拡張可能スイッチのドライバー スタックにバインドされると、オペレーティング システム、SR-IOV または VMQ のいずれかの機能の使用を有効にします。

    HYPER-V 拡張可能スイッチの詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチ](hyper-v-extensible-switch.md)します。

ネットワーク アダプターが、TCP/IP スタックと、HYPER-V 拡張可能スイッチのドライバー スタックからバインドできない場合は、ミニポート ドライバーが停止され、し、再初期化します。 このため、RSS、VMQ、SR-IOV 対応の間に自動的に切り替えるには、このようなネットワーク アダプターのことはできません。

NDIS を呼び出すと、 [ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数、ミニポート ドライバーこれらの手順に従う NDIS に、現在有効になっている、SR-IOV、VMQ、または RSS の機能を報告する前に。

1.  ミニポート ドライバーの読み込み、  **\*SriovPreferred** NDIS を現在有効な機能を報告する前にキーワード。

    場合の値、  **\*SriovPreferred**キーワードは、1 つ、ミニポート ドライバーが SR-IOV 対応の基本設定の構成します。

2.  ミニポート ドライバーの読み込み、  **\*RssOrVmqPreference** NDIS を現在有効な機能を報告する前にキーワード。

    場合の値、  **\*RssOrVmqPreference**キーワードは、1 つ、VMQ の基本設定が構成されているミニポート ドライバー。

    場合の値、  **\*RssOrVmqPreference**キーワードは、0 またはキーワードが存在しない、RSS の基本設定が構成されているミニポート ドライバー。

3.  これを読み取る必要があるかどうかミニポート ドライバーが SR-IOV 対応の基本設定の構成で、  **\*SRIOV**ネットワーク アダプターで SR-IOV が有効になっているかどうかを決定するキーワード。 キーワードは、いずれかに設定されている場合、ドライバーは現在有効になっている SR-IOV 設定を報告します。

    ミニポート ドライバーが SR-IOV 設定を報告する方法の詳細については、次を参照してください。 [SR-IOV 機能を決定する](determining-sr-iov-capabilities.md)します。

    SR-IOV キーワードの詳細については、次を参照してください。 [SR-IOV の標準化された INF キーワード](standardized-inf-keywords-for-sr-iov.md)します。

    **注**  キーワードを標準化、RSS のいずれかを読み取り、ミニポート ドライバーが SR-IOV 対応の基本設定で構成された場合いない必要があります。 ただし、ドライバーは、VMQ を読み取る必要があります **\*VMQVlanFiltering**標準化されたキーワードです。 このキーワードは、ミニポート ドライバーがメディア アクセス制御 (MAC) ヘッダーで仮想の VLAN (VLAN) id を使用してネットワーク パケットをフィルター処理を有効になっているかどうかを指定します。 ミニポート ドライバーでは、この機能を報告するには、NDIS\_受信\_フィルター\_MAC\_ヘッダー\_VLAN\_ID\_でサポートされているフラグ、 **SupportedMacHeaderFields**のメンバー、 [ **NDIS\_受信\_フィルター\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)構造体。 詳細については、  **\*VMQVlanFiltering**標準化されたキーワードを参照してください[VMQ の標準化された INF キーワード](standardized-inf-keywords-for-vmq.md)します。

     

4.  それを読み取る必要があるかどうかミニポート ドライバーは VMQ の基本設定の構成で、  **\*VMQ**ネットワーク アダプターで VMQ が有効になっているかどうかを決定するキーワード。 キーワードは、いずれかに設定されている場合、ドライバーは現在有効になっている VMQ 設定を報告します。 ミニポート ドライバーで VMQ 設定を報告する方法の詳細については、次を参照してください。[ネットワーク アダプターの VMQ 機能を判断する](determining-the-vmq-capabilities-of-a-network-adapter.md)します。

    VMQ キーワードの詳細については、次を参照してください。 [VMQ の標準化された INF キーワード](standardized-inf-keywords-for-vmq.md)します。

    **注**  ミニポート ドライバーは VMQ の基本設定を構成する場合にする必要がありますを読み取れません RSS または SR-IOV 対応のいずれかのキーワードを標準化します。

     

5.  これを読み取る必要があるかどうかは、RSS の基本設定のミニポート ドライバーが構成されている、  **\*RSS**ネットワーク アダプターで RSS が有効になっているかどうかを決定するキーワード。 キーワードは、いずれかに設定されている場合、ドライバーは現在有効な RSS 設定を報告します。 ミニポート ドライバーが RSS の設定を報告する方法の詳細については、次を参照してください。 [RSS 構成](rss-configuration.md)します。

    RSS キーワードの詳細については、次を参照してください。[の RSS の標準化された INF キーワード](standardized-inf-keywords-for-rss.md)します。

    **注**  ミニポート ドライバーは RSS の基本設定を構成する場合にする必要がありますを読み取れません VMQ または SR-IOV 対応のいずれかのキーワードを標準化します。

     

次の表では、ミニポート ドライバーが、ネットワーク アダプターで適切なインターフェイスを有効にするには、SR-IOV、VMQ、または RSS の基本設定を決定する方法について説明します。

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
<th align="left"><em>SriovPreferred</th>
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
<td align="left"><p>なし</p></td>
<td align="left"><p>SR-IOV と VMQ</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>なし</p></td>
<td align="left"><p>VMQ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>1、0、またはレジストリに存在しません</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>なし</p></td>
<td align="left"><p>なし</p></td>
</tr>
<tr class="even">
<td align="left"><p>0 の場合、またはレジストリに存在しません</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>なし</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>なし</p></td>
<td align="left"><p>VMQ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0 の場合、またはレジストリに存在しません</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>なし</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>なし</p></td>
<td align="left"><p>なし</p></td>
</tr>
<tr class="even">
<td align="left"><p>0 の場合、またはレジストリに存在しません</p></td>
<td align="left"><p>0 の場合、またはレジストリに存在しません</p></td>
<td align="left"><p>なし</p></td>
<td align="left"><p>なし</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>RSS</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0 の場合、またはレジストリに存在しません</p></td>
<td align="left"><p>0 の場合、またはレジストリに存在しません</p></td>
<td align="left"><p>なし</p></td>
<td align="left"><p>なし</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>なし</p></td>
</tr>
</tbody>
</table>

 

**注**  ときの SR-IOV 対応および VMQ インターフェイスの両方が有効、SR-IOV 既定以外のバーチャル ポート (拡張) を PCI Express (PCIe) 物理機能 (PF) にアタッチされているが VMQ インターフェイスの VM のキューの代わりに使用します。 詳細については、次を参照してください。[既定以外の仮想ポートおよび VMQ](nondefault-virtual-ports-and-vmq.md)します。

 

ミニポート ドライバーでは、現在有効なインターフェイスの機能を提供する必要があります。 たとえば、SR-IOV が有効になっている場合、ミニポート ドライバーする必要がありますアドバタイズ SR-IOV 機能が機能しない VMQ または RSS。 ただし、ミニポート ドライバーが、ネットワーク アダプターに関係なく、インターフェイスが有効になって完了の RSS、VMQ、SR-IOV 対応ハードウェアの機能を常に報告する必要があります。

**注**  VMQ と SR-IOV のインターフェイスを使用するは、VM キューまたは SR-IOV 仮想ポート (拡張) 経由でフィルター処理を受信します。 フィルター処理結果として、いくつか表示される機能では、同じが必要なまたはインターフェイスのいずれかのときに、さまざまな設定が有効にします。 受信側の SR-IOV インターフェイスのフィルタ リング機能を報告する方法の詳細については、次を参照してください。[受信フィルタ リング機能を決定する](determining-receive-filtering-capabilities.md)します。 VMQ インターフェイスのフィルタ リング機能の受信を報告する方法の詳細については、次を参照してください。[ネットワーク アダプターの VMQ 機能を判断する](determining-the-vmq-capabilities-of-a-network-adapter.md)します。

 

 

 





