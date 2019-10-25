---
title: 物理ネットワーク アダプターからの NDIS 状態表示の転送
description: 物理ネットワーク アダプターからの NDIS 状態表示の転送
ms.assetid: 6EE9BB96-FFAB-4844-9F74-43FB3F18FAB2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 523f539c2b1cf637097700c09aadd14bab08f4e2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841752"
---
# <a name="forwarding-ndis-status-indications-from-physical-network-adapters"></a>物理ネットワーク アダプターからの NDIS 状態表示の転送


このトピックでは、拡張可能なスイッチ転送拡張機能によって使用されるメソッドについて説明します。このメソッドは、基になる物理アダプターから NDIS ステータスの兆候を転送します。 1つまたは複数の基になる物理アダプターを、Hyper-v 拡張可能スイッチの外部ネットワークアダプターにバインドできます。

たとえば、外部ネットワークアダプターは、NDIS マルチプレクサー (MUX) 中間ドライバーの仮想ミニポートエッジにバインドできます。 MUX ドライバーは、ホスト上の1つまたは複数の物理ネットワークのチームにバインドされています。 この構成は、*拡張可能なスイッチチーム*と呼ばれています。

この構成では、拡張可能なスイッチ拡張機能がチーム内のすべてのネットワークアダプターに公開されます。 これにより、拡張機能がチーム内の個々のネットワークアダプターの構成と使用を管理できるようになります。 たとえば、転送拡張機能は、送信パケットを個々のアダプターに転送することによって、チームで負荷分散フェールオーバー (LBFO) ソリューションのサポートを提供できます。 拡張可能なスイッチチームを管理する転送拡張機能は、*チーミングプロバイダー*と呼ばれます。 チーミングプロバイダーの詳細については、「[チーミングプロバイダーの拡張機能](teaming-provider-extensions.md)」を参照してください。

次の図は、ndis 6.40 (Windows Server 2012 R2) の基礎となる物理ネットワークアダプターからの NDIS ステータス表示の Hyper-v 拡張可能スイッチ制御パスを示しています。

![ndis 6.40 の物理ネットワークアダプターからの ndis ステータスインジケーターの vswitch 制御パス](images/vswitch-status-controlpath2-ndis640.png)

次の図は、ndis 6.30 (Windows Server 2012) の基礎となる物理ネットワークアダプターからの NDIS ステータス表示の Hyper-v 拡張可能スイッチ制御パスを示しています。

![ndis 6.30 の物理ネットワークアダプターからの ndis ステータスインジケーターの vswitch 制御パス](images/vswitch-status-controlpath2.png)

**注**  拡張可能なスイッチインターフェイスでは、NDIS フィルタードライバーは拡張*可能なスイッチ拡張機能*と呼ばれ、ドライバースタックは*拡張可能なスイッチドライバースタック*と呼ばれます。

 

拡張可能なスイッチインターフェイスは、基になる物理アダプターによって生成された NDIS ステータスの兆候を転送します。 外部ネットワークアダプターが拡張可能なスイッチチームにバインドされている場合、NDIS の状態は、MUX ドライバーの仮想アダプターのエッジによって示されます。 それ以外の場合、状態は、外部ネットワークアダプターにバインドされている単一の物理ネットワークアダプターによって生成されます。

NDIS ステータスの表示が拡張可能スイッチインターフェイスに到着すると、 [**ndis\_スイッチ\_NIC\_状態\_示さ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_nic_status_indication)れる構造体の内部に示された情報がカプセル化されます。 次に、拡張可能スイッチのミニポートエッジは、この構造を含む[ **\_NIC\_状態を示す\_スイッチの\_の状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-switch-nic-status)を示します。

転送拡張機能は、NDIS ステータス表示を受け取ると、元の表示データを転送するか、またはデータを変更してから指示を転送できます。

状態の表示を転送する前に、転送拡張機能のみがデータを変更できることに**注意**してください  。 この種類の拡張機能の詳細については、「[拡張機能の転送](forwarding-extensions.md)」を参照してください。

 

転送拡張機能は、拡張可能なスイッチの外部ネットワークアダプターにバインドされている、基になる物理アダプターの状態を変更および転送できます。 通常、拡張機能は、これらの状態の兆候を発行して、基盤となる物理アダプターのハードウェアオフロード機能を変更します。 たとえば、拡張機能は、次の種類のハードウェアオフロードについて、状態を変更および転送できます。

-   インターネットプロトコルセキュリティ (IPsec)

-   仮想マシンキュー (VMQ)

-   シングル ルート I/O 仮想化 (SR-IOV)

転送拡張機能が NDIS ステータス表示を転送する場合は、次の方法で、 [**ndis\_スイッチ\_NIC\_状態\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_nic_status_indication)表示構造のメンバーを設定する必要があります。

-   **SourcePortId**メンバーは、外部ネットワークアダプターが接続されているポートの識別子に設定する必要があります。 外部ネットワークアダプターは、1つまたは複数の物理アダプターにバインドされています。 詳細については、「[外部ネットワークアダプター](external-network-adapters.md)」を参照してください。

-   **Sourcenicindex**メンバーは、既定\_\_NIC\_インデックスに設定する必要があります\_に設定する必要があります。 これにより、外部ネットワークアダプターにバインドされている拡張可能なスイッチチーム全体からの状態を示すことができます。

-   **DestinationPortId**メンバーは、**既定\_ポート\_ID に\_スイッチ\_、NDIS**に設定する必要があります。

-   DestinationNicIndex メンバーは、**既定\_NIC\_インデックス**に設定\_、\_に設定する必要があります。

-   **Statusindication**メンバーは、 [**NDIS\_ステータス\_示す**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)構造体へのポインターに設定する必要があります。 この構造体には、カプセル化された NDIS 状態を示すデータが含まれます。

転送拡張機能がカプセル化された NDIS 状態を示す場合は、次の手順に従う必要があります。

1.  拡張機能は参照を参照するための "参照" を呼び出し、外部ネットワークアダプターの参照[*カウンターをインクリメント*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)します。 これにより、拡張可能なスイッチインターフェイスは、参照カウンターが0以外の場合にネットワークアダプター接続を削除しません。

    拡張機能では[ *、* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic) *SwitchPortId*パラメーターが、 **SourcePortId**メンバーに対して指定された値に設定されます。 また、この拡張機能は、 *SwitchNicIndex*パラメーターを**Sourcenicindex**メンバーに指定された値に設定します。

    **注**  は、\_ステータス\_成功しなかっ[*た場合に*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)、カプセル化された ndis ステータスを発行できません。

     

2.  この拡張機能は、 [**NdisFIndicateStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatestatus)を呼び出して、カプセル化された状態通知を転送します。

    **注**  拡張機能がカプセル化された NDIS 状態を転送する場合は、 [*filterstatus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_status)関数の呼び出しのコンテキスト内で[**NdisFIndicateStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatestatus)を呼び出す必要があります。

     

3.  [**NdisFIndicateStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatestatus)が返された後、拡張機能は[*DereferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_nic)を呼び出して、送信元または送信先のネットワークアダプター接続の参照カウンターをクリアします。 この拡張機能は、 *SwitchPortId*パラメーターと*SwitchNicIndex*パラメーターを、の呼び出しで使用したものと同じ値に設定[*します。* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)

MUX ドライバーの詳細については、「 [NDIS MUX 中間ドライバー](ndis-mux-intermediate-drivers.md)」を参照してください。

 

 





