---
title: MSI-X リソース フィルター処理
description: MSI-X リソース フィルター処理
ms.assetid: ccc6aac0-7c89-4e48-ac53-9e3a72965a43
keywords:
- MSI-X WDK ネットワーク, リソース要件フィルター関数
- メッセージシグナル割り込み、WDK ネットワーク、リソース要件フィルター関数
- Msi WDK ネットワーク、リソース要件フィルター関数
- リソース要件フィルター関数 WDK net
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01efd6bc1d50d37ebae7a9a1f90d8ce55dde608f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844211"
---
# <a name="msi-x-resource-filtering"></a>MSI-X リソース フィルター処理





ミニポートドライバーは、MSI-X をサポートする場合はリソース要件フィルター関数を登録する必要があり、各 MSI-X メッセージの割り込み関係を変更するか、メッセージ割り込みリソースを削除します。

Ndis は、NDIS が Irp を受信した後、 [*MiniportFilterResourceRequirements*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pnp_irp)関数を呼び出します。これは、ネットワークインターフェイスカード (NIC) の[ **\_フィルター\_リソース\_要件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-filter-resource-requirements)I/O 要求パケット (irp) を\_します。 NDIS は、デバイススタック内の基になる関数ドライバーが IRP を完了した後に*MiniportFilterResourceRequirements*を呼び出します。

[*MiniportAddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_add_device)関数が ndis\_\_STATUS を返した後、Ndis は*MiniportFilterResourceRequirements*を呼び出しますが、成功します。 *MiniportFilterResourceRequirements*は、 [*Miniportremovedevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_remove_device)を呼び出す前に、いつでも再度呼び出すことができます。 ミニポートの実行中に、NDIS は*MiniportFilterResourceRequirements*を呼び出すことができます。 ミニポートでは、以下に示すようにリソース一覧が変更される場合がありますが、ミニポートでは、新しいリソースの使用をすぐに試みることはできません。 NDIS は、新しいリソースを使用して、最終的にミニポートを停止し、再初期化します。その後、ミニポートで新しいリソースの使用を試みる必要があります。

[**Irp\_\_フィルター\_リソース\_の要件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-filter-resource-requirements)では、 **Irp-\_Iostatus. 情報**の[ **\_リスト構造\_IO&gt;リソース**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_resource_requirements_list)の一覧が提供されます。 一覧のリソースは、 [**IO\_リソース\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_resource_descriptor)の構造によって記述されます。

ミニポートドライバーは、MSI-X メッセージを記述する**Cmresourcetypeinterrupt**型のリソースごとに割り込みアフィニティポリシーを変更できます。 アフィニティポリシーが特定のプロセッサセットのターゲット設定を要求した場合は、ミニ[**アフィニティ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/interrupt-affinity-and-priority#about-kaffinity)マスクも、IO\_リソース\_記述子構造内の割り込みによって設定さ**れます。**

ミニポートドライバーは、メッセージ割り込みリソースである**Cmresourcetypeinterrupt**型のすべてのリソースを削除できます。 ドライバーは、 [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数の行ベースの割り込みに登録できます。 これらのメッセージ割り込みリソースがミニポートドライバーによって削除されない場合、ドライバーが*MiniportInitializeEx*に行ベースの割り込みを登録しようとすると、オペレーティングシステムは失敗します。

NDIS 6.1 以降のミニポートドライバーでは、リソースの一覧にメッセージ割り込みリソースを追加できます。 たとえば、8個の Cpu を搭載したコンピューターで、NIC が4つの MSI-X メッセージを生成でき、オペレーティングシステムで4つのメッセージ割り込みが有効になっている場合、オペレーティングシステムはデバイスの MSI-X 構成領域で4つのメッセージテーブルエントリを初期化し、4つのリソース一覧のメッセージ割り込みリソース。 この場合、ミニポートドライバーでは、より多くのメッセージ割り込みリソースが必要になるため、4つのメッセージ割り込みリソースをリソースリストに割り当て、各 MSI-X メッセージの関係を CPU に設定することができます。 オペレーティングシステムがより多くのメッセージ割り込みリソースを提供できる場合、ミニポートアダプターは、開始時に8個のメッセージ割り込みリソースを受け取ります。 この場合、メッセージには 0 ~ 7 の数値が含まれます。

リスト内の各メッセージ割り込みリソースには、後で一覧に表示される順序に対応するメッセージ番号が割り当てられます。 たとえば、リスト内の最初のメッセージ割り込みリソースは、メッセージ0に割り当てられ、2つ目のメッセージはメッセージ1に割り当てられます。

実行時に MSI-X テーブルのエントリを CPU に割り当てるために、ミニポートドライバーは[**NdisMConfigMSIXTableEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismconfigmsixtableentry)関数を呼び出すことができます。この関数は、既に関係が CPU に設定されている Msi-x メッセージにテーブルエントリをマップします。 MSI-X のテーブルエントリの構成操作の詳細については、「 [msi-x テーブルエントリの CPU 関係の変更](changing-the-cpu-affinity-of-msi-x-table-entries.md)」を参照してください。

新しいリソース要件の一覧にメモリを割り当てるには、 [**NdisAllocateMemoryWithTagPriority**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatememorywithtagpriority)関数を使用します。 [**NdisFreeMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreememory)関数を使用すると、以前のリソース要件の一覧のメモリを解放できます。

ミニポートドライバーは、 **CmResourceTypeMemory**や**Cmresourcetypeport**リソースなどの他のリソースを変更しないでください。 ミニポートドライバーは、リソースの一覧に新しいリソースを追加しないようにする必要があります。 ただし、NDIS 6.1 以降のミニポートドライバーでは、より多くのメッセージ割り込みリソースを追加できます。 ミニポートドライバーにより多くのメッセージ割り込みリソースが追加される場合は、 [*Miniportstartdevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pnp_irp)関数から削除しないでください。

リソースの追加と削除の詳細については、「 [**IRP\_\_フィルター\_リソース\_の要件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-filter-resource-requirements)」を参照してください。

