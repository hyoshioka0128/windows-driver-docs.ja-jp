---
title: MSI-X リソース フィルター処理
description: MSI-X リソース フィルター処理
ms.assetid: ccc6aac0-7c89-4e48-ac53-9e3a72965a43
keywords:
- MSI X の WDK ネットワーク、リソース要件をフィルター処理関数
- メッセージ シグナル割り込み WDK ネットワーク、リソース要件フィルター関数
- Msi WDK ネットワーク、リソース要件フィルター関数
- リソース要件関数 net WDK をフィルター処理します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0e18dc5708f0e36b58092e464340391bc7dab85
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582436"
---
# <a name="msi-x-resource-filtering"></a>MSI-X リソース フィルター処理





ミニポート ドライバーは、MSI をサポートし、MSI X メッセージごとに割り込みアフィニティを変更またはメッセージの割り込みのリソースが削除される場合、リソース要件フィルター関数を登録する必要があります。

NDIS 呼び出し、 [ *MiniportFilterResourceRequirements* ](https://msdn.microsoft.com/library/windows/hardware/ff559384)関数 NDIS を受信した後、 [ **IRP\_MN\_フィルター\_リソース\_要件**](https://msdn.microsoft.com/library/windows/hardware/ff550874)ネットワーク インターフェイス カード (NIC) の I/O 要求パケット (IRP)。 NDIS 呼び出し*MiniportFilterResourceRequirements*デバイス スタックの基になる関数ドライバーは IRP を完了した後。

NDIS が呼び出す*MiniportFilterResourceRequirements*後、 [ *MiniportAddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff559332) NDIS を返します\_状態\_成功します。 NDIS を呼び出すことが*MiniportFilterResourceRequirements*呼び出す前にいつでも再び[ *MiniportRemoveDevice*](https://msdn.microsoft.com/library/windows/hardware/ff559427)します。 NDIS を呼び出すことが*MiniportFilterResourceRequirements*ミニポートの実行中にします。 ミニポートは、以下に示すようにリソースの一覧を変更可能性があります、ミニポートすぐにしようとしないでください、新しいリソースを使用します。 NDIS は最終的に停止し、新しいリソースにミニポートを再初期化、新しいリソースを使用するミニポートが試みる必要があるはその後。

[**IRP\_MN\_フィルター\_リソース\_要件**](https://msdn.microsoft.com/library/windows/hardware/ff550874)とリソースの一覧を提供する[ **IO\_リソース\_要件\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff550609)で構造体**Irp -&gt;IoStatus.Information**します。 一覧内のリソースが記載されている[ **IO\_リソース\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff550598)構造体。

ミニポート ドライバーは、各リソースの種類の割り込みアフィニティ ポリシーを変更する**CmResourceTypeInterrupt** MSI X メッセージについて説明します。 アフィニティのポリシーを特定の対象とするプロセッサのミニポート ドライバーも設定セットを要求する場合、 [ **KAFFINITY** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/interrupt-affinity-and-priority#about-kaffinity)でマスク**Interrupt.TargetedProcessors**で、IO\_リソース\_記述子構造体。

ミニポート ドライバーは、型のすべてのリソースを削除できます**CmResourceTypeInterrupt**メッセージ割り込みリソースであります。 割り込みの行ベースのドライバーを登録できますし、 [ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数。 ミニポート ドライバーがこれらのメッセージ割り込みリソースを削除しない場合、ドライバーで線ベースの割り込みを登録しようとする場合に、オペレーティング システムは失敗*MiniportInitializeEx*します。

NDIS 6.1 または以降のバージョンのミニポート ドライバーは、リソースの一覧にメッセージの割り込みのリソースを追加できます。 8 個の cpu を搭載したコンピューター上など、NIC が MSI X の 4 つのメッセージを生成し、オペレーティング システムで 4 つのメッセージ割り込み場合、オペレーティング システム、デバイスの MSI X 構成領域の 4 つのメッセージ テーブル エントリを初期化し、4 は、リソースの一覧でメッセージ割り込みリソース。 ここでは、ミニポート ドライバーには、メッセージの割り込みの他のリソースが必要であるため割り込みリソース、リソースの一覧を次の 4 つ以上のメッセージを割り当てるし、CPU に MSI X の各メッセージのアフィニティを設定できます。 オペレーティング システムがメッセージの割り込みの他のリソースを提供できる場合、ミニポート アダプターは、実行しているメッセージ割り込みの 8 つのリソースを受信します。 この場合、メッセージには、0 ~ 7 の数字があります。

リスト内の各メッセージ割り込みリソースには、一覧の表示順序をメッセージ番号を後で対応するが割り当てられます。 たとえば、最初のメッセージ割り込みリソースの一覧では、0 をメッセージに割り当てられている、して、メッセージ 1、2 つ目が割り当てられます。

実行時に、CPU に MSI X テーブル エントリを割り当てる、ミニポート ドライバーを呼び出すことができます、 [ **NdisMConfigMSIXTableEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff563566)関数で、テーブル エントリに関係セットが既にいる MSI X メッセージ マップCPU。 MSI X テーブル エントリの構成操作の詳細については、[MSI X テーブル エントリの CPU 関係を変更する](changing-the-cpu-affinity-of-msi-x-table-entries.md)を参照してください。

新しいリソース要件の一覧については、メモリを割り当て、使用、 [ **NdisAllocateMemoryWithTagPriority** ](https://msdn.microsoft.com/library/windows/hardware/ff561606)関数。 古いリソース要件の一覧については、メモリを解放することができます、 [ **NdisFreeMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff562577)関数。

ミニポート ドライバーがなどその他のリソースを変更しない必要があります**CmResourceTypeMemory**と**CmResourceTypePort**リソース。 ミニポート ドライバーでは、リソースの一覧に新しいリソースを追加することを避ける必要があります。 ただし、NDIS 6.1 と以降のミニポート ドライバーでは、メッセージの割り込みの他のリソースを追加できます。 ミニポート ドライバーでは、メッセージの割り込みの他のリソースを追加する場合、削除しないでから、 [ *MiniportStartDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff559452)関数。

追加して、リソースの削除の詳細については、[ **IRP\_MN\_フィルター\_リソース\_要件**](https://msdn.microsoft.com/library/windows/hardware/ff550874)を参照してください。

