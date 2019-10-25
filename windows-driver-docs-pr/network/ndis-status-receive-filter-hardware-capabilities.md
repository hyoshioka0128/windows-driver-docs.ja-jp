---
title: NDIS_STATUS_RECEIVE_FILTER_HARDWARE_CAPABILITIES
description: ミニポートドライバーは、ハードウェアの受信フィルター機能が変更されたときに、NDIS_STATUS_RECEIVE_FILTER_HARDWARE_CAPABILITIES 状態を示します。
ms.assetid: 12F7A736-D85A-4BB6-89E6-55195B76C29F
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_RECEIVE_FILTER_HARDWARE_CAPABILITIES ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: f0561105d7ef94ebd36d905f8b13b134f7054e69
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843523"
---
# <a name="ndis_status_receive_filter_hardware_capabilities"></a>NDIS\_ステータス\_\_フィルター\_ハードウェア\_機能


ミニポートドライバーは、ハードウェアの受信フィルター処理機能が変更された場合に **\_ハードウェア\_機能の状態を示す\_フィルターを受信\_NDIS\_の状態**を発行します。 これらの機能には、現在 INF ファイルの設定によって無効にされているハードウェア機能や、 **[詳細設定**] プロパティページがあります。

この状態の表示は、NDIS 受信フィルターをサポートするミニポートドライバーによってのみ行う必要**が  ます**。

 

ミニポートドライバーによってこの状態が表示されると、 [**ndis\_ステータス\_示さ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)れる構造体の**statusbuffer**メンバーが\_ndis へのポインターに設定[**され\_フィルター\_機能を受け取る**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)ようになります。データ. ドライバーは、現在有効になっている受信フィルター機能を使用して、この構造体を初期化します。

<a name="remarks"></a>注釈
-------

NDIS 受信フィルターは、次の NDIS インターフェイスで使用されます。

-   [NDIS パケット合体](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-packet-coalescing)。 このインターフェイスで受信フィルターを使用する方法の詳細については、「[パケット合体受信フィルターの管理](https://docs.microsoft.com/windows-hardware/drivers/network/managing-packet-coalescing-receive-filters)」を参照してください。

-   [シングルルート I/o 仮想化 (sr-iov)](https://docs.microsoft.com/windows-hardware/drivers/network/single-root-i-o-virtualization--sr-iov-)。 このインターフェイスで受信フィルターを使用する方法の詳細については、「[仮想ポートでの受信フィルターの設定](https://docs.microsoft.com/windows-hardware/drivers/network/setting-a-receive-filter-on-a-virtual-port)」を参照してください。

-   [仮想マシン キュー (VMQ)](https://docs.microsoft.com/windows-hardware/drivers/network/virtual-machine-queue--vmq--in-ndis-6-20)。 このインターフェイスで受信フィルターを使用する方法の詳細については、「 [VMQ フィルターの設定とクリア](https://docs.microsoft.com/windows-hardware/drivers/network/setting-and-clearing-vmq-filters)」を参照してください。

ミニポートドライバーは、次のいずれかの条件に該当する場合に **\_ハードウェア\_機能の状態を示す\_フィルターを受信\_NDIS\_の状態**を発行します。

-   ハードウェアの受信フィルター機能が、1つのネットワークアダプターで変更されます。 たとえば、受信フィルターは、独立系ハードウェアベンダー (IHV) によって開発された管理アプリケーションを使用して有効または無効にすることができます。

-   ハードウェアの受信フィルター機能は、MUX 中間ドライバーによって管理されるネットワークアダプターの負荷分散フェールオーバー (LBFO) チームに対して変更されます。 たとえば、ハードウェアの受信フィルター機能は、アダプターをチームに追加したり、チームから削除したりすると変更される可能性があります。

    詳細については、「 [NDIS MUX 中間ドライバー](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-mux-intermediate-drivers)」を参照してください。

ミニポートドライバーは、次の手順に従って、 **NDIS\_ステータス\_受信\_フィルター\_ハードウェア\_機能**の状態を示します。

1.  ミニポートは、ネットワークアダプターで現在有効になっている受信フィルター機能を使用して、 [ **\_フィルター\_機能の構造を受け取る NDIS\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)を初期化します。

    ミニポートドライバーは、**ヘッダー**メンバーを初期化するときに、**ヘッダー**の**TYPE**メンバーを NDIS\_OBJECT\_type\_DEFAULT に設定します。 ミニポートドライバーは、**ヘッダー**の**リビジョン**メンバーを NDIS\_受信\_フィルター\_機能\_リビジョン\_2 および**SIZE**メンバーを ndis\_SIZEOF\_receive に設定\_リビジョン\_2\_\_機能をフィルター処理します。

2.  ミニポートドライバーは、次の方法で状態を示すように、 [**NDIS\_ステータス\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)構造体を初期化します。

    -   **StatusCode**メンバーを NDIS\_STATUS に設定し、 [ **\_フィルター\_現在の\_機能を受信\_** ](ndis-status-receive-filter-current-capabilities.md)する必要があります。

    -   **Statusbuffer**メンバーは、 [**NDIS\_RECEIVE\_FILTER\_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)構造体のアドレスに設定する必要があります。

    -   **Statusbuffersize**メンバーを `sizeof(NDIS_RECEIVE_FILTER_CAPABILITIES)`に設定する必要があります。

3.  ミニポートドライバーは、 [**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)を呼び出すことによって状態を示します。 ドライバーは、 [**NDIS\_STATUS\_を示す**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)ポインターを*statusindication*パラメーターに渡す必要があります。

**注**  は、NDIS\_ステータスを使用して **\_フィルターを受信\_\_ハードウェア\_機能**の状態を表示し、現在有効になっている受信フィルター機能を特定します。ネットワークアダプター。 また、これらのドライバーは、ハードウェアの受信フィルター機能をいつでも取得できるように、[ハードウェア\_機能を受信\_フィルター\_\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-hardware-capabilities) OID の oid クエリ要求を発行することもできます。

 

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>NDIS 6.30 以降でサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis .h (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


****
[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)

[**NDIS\_状態\_表示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[**NDIS\_受信\_フィルター\_の機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)

[OID\_現在の\_機能\_受信\_フィルター処理](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-current-capabilities)

 

 




