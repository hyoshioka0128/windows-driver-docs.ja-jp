---
title: 物理ネットワーク アダプターからの NDIS 状態表示の転送
description: 物理ネットワーク アダプターからの NDIS 状態表示の転送
ms.assetid: 6EE9BB96-FFAB-4844-9F74-43FB3F18FAB2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fcebb16461d63e52b4be8a510266f9f910e1aca3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353340"
---
# <a name="forwarding-ndis-status-indications-from-physical-network-adapters"></a>物理ネットワーク アダプターからの NDIS 状態表示の転送


このトピックでは、転送拡張機能を基になる物理アダプターから前方 NDIS 状態インジケーターに拡張可能スイッチで使用されるメソッドを説明します。 1 つ以上の物理アダプターを基になるは、HYPER-V 拡張可能スイッチの外部ネットワーク アダプターにバインドできます。

たとえば、外部ネットワーク アダプターは、NDIS マルチプレクサー (マルチプレクサー) の中間ドライバーの仮想ミニポート端にバインドできます。 MUX driver は、ホスト上の 1 つまたは複数の物理ネットワーク チームにバインドされます。 この構成と呼ばれる、*拡張可能スイッチ チーム*します。

この構成で拡張可能スイッチの拡張機能は、チーム内のすべてのネットワーク アダプターに公開されます。 これにより、拡張機能の構成と、チーム内の個々 のネットワーク アダプターの使用を管理できます。 たとえば、転送拡張機能では、個々 のアダプターに送信されるパケットを転送することによって、over、チーム分散フェールオーバー (LBFO) のソリューション ロードのサポートを提供できます。 拡張可能スイッチ チームを管理する転送拡張機能が呼ばれる、*チーミング プロバイダー*します。 プロバイダーのチーミングの詳細については、次を参照してください。[プロバイダーの拡張機能のチーミング](teaming-provider-extensions.md)します。

次の図では、NDIS 6.40 (Windows Server 2012 R2) と後で、基になる物理ネットワーク アダプターから NDIS 状態インジケーターの HYPER-V 拡張可能スイッチ コントロール パスが表示されます。

![ndis 6.40 の物理ネットワーク アダプターから ndis 状態インジケーターの vswitch コントロール パス](images/vswitch-status-controlpath2-ndis640.png)

次の図は、NDIS 6.30 (Windows Server 2012) の基になる物理ネットワーク アダプターから NDIS 状態インジケーターの HYPER-V 拡張可能スイッチ コントロールのパスを示します。

![ndis 6.30 の物理ネットワーク アダプターから ndis 状態インジケーターの vswitch コントロール パス](images/vswitch-status-controlpath2.png)

**注**  、拡張可能スイッチのインターフェイスで NDIS フィルター ドライバーと呼ばれる*拡張可能スイッチの拡張機能*と呼ばれるドライバー スタック、*拡張可能スイッチ ドライバー スタック*.

 

拡張可能スイッチのインターフェイスは、基になる物理アダプターによって生成された NDIS 状態インジケーターを転送します。 外部ネットワーク アダプターは、拡張可能スイッチ チームにバインドする場合は、MUX driver の仮想アダプターの端で NDIS 状態の表示が開始されます。 それ以外の場合、外部ネットワーク アダプターにバインドされている 1 つの物理ネットワーク アダプターで状態の表示が開始されます。

拡張可能スイッチのインターフェイスで NDIS 状態を示す値が到着すると、内で示す値をカプセル化、 [ **NDIS\_切り替える\_NIC\_状態\_を示す値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_nic_status_indication)構造体。 拡張可能スイッチに関する問題のミニポート edge し、 [ **NDIS\_状態\_スイッチ\_NIC\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-switch-nic-status)これを含むことを示しています構造体。

転送拡張機能が、NDIS 状態を示す値を受け取ると、元の表示データを転送も示す値を転送する前に、データを変更できます。

**注**  だけが、状態を示す値を転送する前に、データを変更できる転送拡張機能。 この種類の拡張機能の詳細については、次を参照してください。[転送拡張機能](forwarding-extensions.md)します。

 

転送拡張機能では、変更でき、拡張可能スイッチの外部ネットワーク アダプターにバインドされている任意の基になる物理アダプターから状態インジケーターを転送することができます。 通常、拡張機能は、基になる物理アダプターのアドバタイズされたハードウェア オフロード機能を変更するには、これら状態インジケーターを発行します。 たとえば、拡張機能は、変更して、ハードウェア オフロードの次の種類の状態インジケーターを転送します。

-   インターネット プロトコル セキュリティ (IPsec)

-   仮想マシン キュー (VMQ)

-   シングル ルート I/O 仮想化 (SR-IOV)

メンバーを設定する必要があります、転送拡張機能では、NDIS 状態を示す値の転送の場合、 [ **NDIS\_スイッチ\_NIC\_状態\_INDICATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_nic_status_indication)次のように構造体。

-   **SourcePortId**メンバーは、外部ネットワーク アダプターが接続されているポートの識別子を設定する必要があります。 外部ネットワーク アダプターは、1 つまたは複数の物理アダプターにバインドされます。 詳細については、次を参照してください。[外部ネットワーク アダプター](external-network-adapters.md)します。

-   **SourceNicIndex** NDIS にメンバーを設定する必要があります\_スイッチ\_既定\_NIC\_インデックス。 これにより、外部ネットワーク アダプターにバインドされている全体の拡張可能スイッチ チームからのものとして解釈される状態の表示ができます。

-   **DestinationPortId**にメンバーを設定する必要があります**NDIS\_スイッチ\_既定\_ポート\_ID**します。

-   **DestinationNicIndex**にメンバーを設定する必要があります**NDIS\_スイッチ\_既定\_NIC\_インデックス**します。

-   **StatusIndication**へのポインターにメンバーを設定する必要があります、 [ **NDIS\_状態\_INDICATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)構造体。 この構造体には、カプセル化された NDIS 状態表示のデータが含まれています。

転送拡張機能がカプセル化された NDIS 状態表示を発行すると、次の手順に従う必要があります。

1.  拡張機能の呼び出し[ *ReferenceSwitchNic* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_reference_switch_nic)を外部ネットワーク アダプターの参照カウンターをインクリメントします。 これにより、エントリの中に、その参照カウンターが 0 以外の場合、拡張可能スイッチのインターフェイスはネットワーク アダプターの接続が削除されません。

    拡張機能を呼び出すと[ *ReferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_reference_switch_nic)、設定、 *SwitchPortId*パラメーターに指定された値を**SourcePortId**メンバー。 また、拡張機能、設定、 *SwitchNicIndex*パラメーターに指定された値を**SourceNicIndex**メンバー。

    **注**  場合[ *ReferenceSwitchNic* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_reference_switch_nic) NDIS を返さない\_状態\_成功した場合、カプセル化された NDIS 状態表示を発行することはできません.

     

2.  拡張機能の呼び出し[ **NdisFIndicateStatus** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfindicatestatus)をカプセル化された状態の通知を転送します。

    **注**  呼び出す必要がありますが、拡張機能は、カプセル化された NDIS 状態を示す値を転送は場合、 [ **NdisFIndicateStatus** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfindicatestatus)そのへの呼び出しのコンテキスト内で[ *FilterStatus* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_status)関数。

     

3.  後[ **NdisFIndicateStatus** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfindicatestatus)拡張機能の呼び出しから返される[ *DereferenceSwitchNic* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_dereference_switch_nic)の参照カウンターをオフにします送信元または送信先のネットワーク アダプター接続します。 拡張機能セット、 *SwitchPortId*と*SwitchNicIndex*を同じパラメーター値への呼び出しで使用されるその it [ *ReferenceSwitchNic* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_reference_switch_nic).

MUX ドライバーの詳細については、次を参照してください。 [NDIS MUX 中間ドライバー](ndis-mux-intermediate-drivers.md)します。

 

 





