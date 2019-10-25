---
title: 物理ネットアダプターからの元の NDIS ステータスのインジケーター
description: 物理ネットワーク アダプターからの NDIS 状態表示の生成
ms.assetid: D588CD7E-98A3-4BA8-A467-6492DA2186CA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9a65f56229bb38114cf9f5d6fc7a58cf34d83ff
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843759"
---
# <a name="originating-ndis-status-indications-from-physical-network-adapters"></a>物理ネットワーク アダプターからの NDIS 状態表示の生成


このトピックでは、スイッチに接続されているネットワークアダプターの NDIS ステータスを示すために拡張可能なスイッチ転送拡張機能によって使用される方法について説明します。 拡張機能は、次の種類のアダプターに対して NDIS ステータスを示すことができます。

-   拡張可能スイッチの[外部ネットワークアダプター](external-network-adapters.md)にバインドされている、1つまたは複数の基になる物理アダプター。

    たとえば、外部ネットワークアダプターは、NDIS マルチプレクサー (MUX) 中間ドライバーの仮想ミニポートエッジにバインドできます。 MUX ドライバーは、ホスト上の1つまたは複数の物理ネットワークのチームにバインドされています。 この構成は、*拡張可能なスイッチチーム*と呼ばれています。

    この構成では、拡張可能なスイッチ拡張機能がチーム内のすべてのネットワークアダプターに公開されます。 これにより、拡張機能がチーム内の個々のネットワークアダプターの構成と使用を管理できるようになります。 たとえば、転送拡張機能は、送信パケットを個々のアダプターに転送することによって、チームで負荷分散フェールオーバー (LBFO) ソリューションのサポートを提供できます。 拡張可能なスイッチチームを管理する転送拡張機能は、*チーミングプロバイダー*と呼ばれます。 チーミングプロバイダーの詳細については、「[チーミングプロバイダーの拡張機能](teaming-provider-extensions.md)」を参照してください。

-   Hyper-v 子パーティション内で公開され、拡張可能なスイッチポートに接続されている仮想マシン (VM) ネットワークアダプター。

次の図は、ndis 6.40 (Windows Server 2012 R2) 以降の物理ネットワークアダプターと VM ネットワークアダプターからの NDIS ステータス表示の Hyper-v 拡張可能スイッチ制御パスを示しています。

![ndis 6.40 以降の物理および vm ネットワークアダプターからの ndis 状態を示す vswitch 制御パス](images/vswitch-status-controlpath3-ndis640.png)

次の図は、NDIS 6.30 (Windows Server 2012) の物理ネットワークアダプターと VM ネットワークアダプターからの NDIS ステータス表示の Hyper-v 拡張可能スイッチ制御パスを示しています。

![ndis 6.30 の物理ネットワークアダプターと vm ネットワークアダプターからの ndis ステータスを示す vswitch 制御パス](images/vswitch-status-controlpath3.png)

**注**  拡張可能なスイッチインターフェイスでは、NDIS フィルタードライバーは*拡張機能*と呼ばれ、ドライバースタックは*拡張可能なスイッチドライバースタック*と呼ばれます。

 

転送拡張機能は、拡張可能なスイッチドライバースタックで、カプセル化されたハードウェアオフロードステータスの兆候を、さらにドライバーに送信できます。 これにより、拡張機能では、拡張可能なスイッチの外部ネットワークアダプターにバインドされている物理アダプターの基になるチームの現在のオフロード機能を変更することもできます。 アダプターのチームが外部ネットワークアダプターにバインドされている場合、NDIS またはそれ以降のプロトコルとフィルタードライバーに提供されるのは、チームの共通機能のみです。 拡張機能を使用すると、チーム内の一部のアダプターでサポートされている機能をアドバタイズすることで、アドバタイズされた機能を拡張できます。 たとえば、拡張機能は、カプセル化された NDIS\_の状態を発行して[ **\_フィルター\_現在の\_機能**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-receive-filter-current-capabilities)に関する情報を受け取り\_チーム全体で現在有効になっている受信フィルターの機能を変更できます。

**注**  転送拡張機能のみがカプセル化された状態を示すことができます。 この種類の拡張機能の詳細については、「[拡張機能の転送](forwarding-extensions.md)」を参照してください。

 

通常、転送拡張機能は、カプセル化された NDIS ステータスのインジケーターを生成して、基になる物理アダプターのアドバタイズされたハードウェアオフロード機能を変更します。 たとえば、拡張機能は、次の種類のハードウェアオフロードの状態を示すことができます。

-   インターネットプロトコルセキュリティ (IPsec)。

-   仮想マシンキュー (VMQ)。

-   シングル ルート I/O 仮想化 (SR-IOV)。

また、転送拡張機能は、カプセル化された NDIS 状態のインジケーターを生成して、Hyper-v 子パーティションに割り当てられているハードウェアオフロードリソースを変更することもできます。 NDIS 6.30 以降では、拡張機能は、カプセル化された NDIS\_状態を発行して[ **\_\_\_ポート\_切り替え**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-switch-port-remove-vf)ます。これにより、VM ネットワークアダプターと PCI Express (PCIe) 仮想関数 (VF)。 VF は、[シングルルート i/o 仮想化 (sr-iov)](single-root-i-o-virtualization--sr-iov-.md)インターフェイスをサポートする、基になる物理ネットワークアダプターによって公開およびサポートされます。

転送拡張機能が、基になる物理アダプターのハードウェアオフロードリソースについて、カプセル化された NDIS 状態を示すものである場合は、Ndis\_スイッチのメンバーを設定する必要があります[ **\_NIC\_状態\_表示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_nic_status_indication)構造体は次のようになります。

-   **DestinationPortId**メンバーは、**既定\_ポート\_ID に\_スイッチ\_、NDIS**に設定する必要があります。
-   DestinationNicIndex メンバーは、**既定\_NIC\_インデックス\_** 、\_に設定する必要があります。

-   **SourcePortId**メンバーは、外部ネットワークアダプターが接続される拡張可能なスイッチポートの識別子に設定する必要があります。

-   **Sourcenicindex**メンバーは、**既定\_\_NIC\_インデックス**に設定する必要があります\_に設定する必要があります。 これにより、外部ネットワークアダプターにバインドされている拡張可能なスイッチチーム全体からの状態を示すことができます。

    また、転送拡張機能では、1つの物理ネットワークアダプターが外部ネットワークアダプターにバインドされている場合にのみ、このメンバーを**NDIS\_SWITCH\_既定\_NIC\_インデックス**に設定する必要がある**ことに注意**してください  。

     

-   **Statusindication**メンバーは、 [**NDIS\_ステータス\_示す**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)構造体へのポインターに設定する必要があります。 この構造体には、カプセル化された NDIS 状態を示すデータが含まれます。

転送拡張機能が、Hyper-v 子パーティションのハードウェアオフロードリソースに対して NDIS 状態を示すものである場合、 [**ndis\_スイッチ\_NIC\_状態\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_nic_status_indication)表示構造のメンバーを設定する必要があります。次のようにします。

-   **DestinationPortId**メンバーと**DestinationNicIndex**メンバーは、パーティションによって使用されるネットワーク接続のポートおよびネットワークアダプターインデックスの対応する値に設定されている必要があります。

-   **SourcePortId**メンバーは、**既定\_ポート\_ID に\_スイッチ\_、NDIS**に設定する必要があります。

-   **Sourcenicindex**メンバーは、**既定\_\_NIC\_インデックス**に設定する必要があります\_に設定する必要があります。

-   **Statusindication**メンバーは、 [**NDIS\_ステータス\_示す**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)構造体へのポインターに設定する必要があります。 この構造体には、カプセル化された NDIS 状態を示すデータが含まれます。

拡張機能がカプセル化された NDIS 状態を示す場合は、次の手順に従う必要があります。

1.  この拡張機能は参照ファイルを呼び出して、ソースまたは宛先のネットワークアダプター接続の参照[*カウンターをインクリメント*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)します。 これにより、拡張可能なスイッチインターフェイスは、参照カウンターが0以外の場合にネットワークアダプター接続を削除しません。

    拡張機能では[ *、次*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)の方法でパラメーターを設定します。

    -   転送拡張機能が、基になる物理アダプターに対してカプセル化された NDIS 状態を示している場合は、 *SwitchPortId*パラメーターを**SourcePortId**メンバーに対して指定された値に設定します。 また、この拡張機能は、 *SwitchNicIndex*パラメーターを**Sourcenicindex**メンバーに指定された値に設定します。

    -   転送拡張機能が Hyper-v 子パーティションの NDIS 状態を示すものである場合は、 *SwitchPortId*パラメーターを**DestinationPortId**メンバーに指定された値に設定します。 また、この拡張機能は、 *SwitchNicIndex*パラメーターを**DestinationNicIndex**メンバーに指定された値に設定します。

    **注**  は、\_ステータス\_成功しなかっ[*た場合に*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)、カプセル化された ndis ステータスを発行できません。

     

2.  この拡張機能は、 [**NdisFIndicateStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatestatus)を呼び出して、カプセル化された状態通知を転送します。

    **注**  フィルター処理された OID 要求を転送する場合は、 [*filterstatus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_status)関数の呼び出しのコンテキスト内で[**NdisFIndicateStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatestatus)を呼び出す必要があります。

     

3.  [**NdisFIndicateStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatestatus)が返された後、拡張機能は[*DereferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_nic)を呼び出して、送信元または送信先のネットワークアダプター接続の参照カウンターをクリアします。 この拡張機能は、 *SwitchPortId*パラメーターと*SwitchNicIndex*パラメーターを、の呼び出しで使用したものと同じ値に設定[*します。* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)

 

 





