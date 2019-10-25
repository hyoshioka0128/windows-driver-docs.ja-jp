---
title: 物理ネットワーク アダプターへの OID 要求の転送
description: 物理ネットワーク アダプターへの OID 要求の転送
ms.assetid: 2A6AA842-FFC2-4CEF-BA56-2FDB277E37C9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19826340aeacaeb7a8367f193684da70ced46f1c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842126"
---
# <a name="forwarding-oid-requests-to-physical-network-adapters"></a>物理ネットワーク アダプターへの OID 要求の転送


このトピックでは、hyper-v 拡張可能スイッチの拡張機能が、基盤となる物理アダプターに対するオブジェクト識別子 (OID) 要求を Hyper-v 拡張可能スイッチの制御パスを介して転送する方法について説明します。 この拡張機能は、このトピックで説明する方法に従って、基になる物理ネットワークアダプターに対して OID 要求を生成することもできます。

たとえば、外部ネットワークアダプターは、NDIS マルチプレクサー (MUX) 中間ドライバーの仮想ミニポートエッジにバインドできます。 MUX ドライバーは、ホスト上の1つまたは複数の物理ネットワークのチームにバインドされています。 この構成は、*拡張可能なスイッチチーム*と呼ばれています。

この構成では、拡張可能なスイッチ拡張機能がチーム内のすべてのネットワークアダプターに公開されます。 これにより、拡張機能がチーム内の個々のネットワークアダプターの構成と使用を管理できるようになります。 たとえば、転送拡張機能は、送信パケットを個々のアダプターに転送することによって、チームで負荷分散フェールオーバー (LBFO) ソリューションのサポートを提供できます。 拡張可能なスイッチチームを管理する転送拡張機能は、*チーミングプロバイダー*と呼ばれます。 チーミングプロバイダーの詳細については、「[チーミングプロバイダーの拡張機能](teaming-provider-extensions.md)」を参照してください。

次の図は、NDIS 6.40 (Windows Server 2012 R2) 以降の拡張可能なスイッチチームの例を示しています。

![ndis 6.40 の oid 制御パスの図](images/vswitch-oid-controlpath2-ndis640.png)

次の図は、NDIS 6.30 (Windows Server 2012) の拡張可能なスイッチチームの例を示しています。

![ndis 6.30 の拡張可能なスイッチチームの図](images/vswitch-oid-controlpath2.png)

**注**  hyper-v 拡張可能スイッチインターフェイスでは、NDIS フィルタードライバーは拡張*可能スイッチ拡張機能*と呼ばれ、ドライバースタックは*拡張可能なスイッチドライバースタック*と呼ばれます。

 

基になる物理ネットワークアダプターに要求を転送するには、OID 要求をカプセル化する必要があります。 OID 要求は、最初に[**NDIS\_スイッチ\_NIC\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request)構造内にカプセル化されます。 次に、oid 要求は、oid [\_スイッチ\_NIC\_要求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)によって、拡張可能なスイッチコントロールパスを通じて転送されます。

基になる物理アダプターに対する OID 要求は、次の方法で発行されます。

<a href="" id="the-extensible-switch-interface-"></a>拡張可能なスイッチインターフェイス。  
ハードウェアオフロード要求などの OID 要求は、次のいずれかの方法で実行されるプロトコルまたはフィルタードライバーによって発行されます。

-   Hyper-v の親パーティションで実行されている管理オペレーティングシステム。

-   Hyper-v 子パーティションで実行されているゲストオペレーティングシステム。

これらの OID 要求は、拡張可能なスイッチによって受信されると、拡張可能なスイッチ制御パスを介してカプセル化され、転送されます。 転送拡張機能は、カプセル化された OID 要求を受信すると、基になる物理アダプターに要求を転送できます。 この機能は、ハードウェアのオフロード用に拡張可能なスイッチチームを構成する場合に特に役立ちます。

たとえば、MUX ドライバーは、拡張可能なスイッチチーム全体の共通機能をアドバタイズします。 ただし、転送拡張機能は OID 要求を発行して、チーム内のアダプターの個々の機能を照会または設定することができます。 次に、転送拡張機能は、外部ネットワークアダプターからの NDIS ステータスを示す情報を生成して、チーム全体に適用される機能についてドライバーに通知します。 この手順の詳細については、「[物理ネットワークアダプターからの元の NDIS ステータス](originating-ndis-status-indications-from-physical-network-adapters.md)の表示」を参照してください。

転送拡張機能は、制御パスで OID 要求を転送するときに、外部ネットワークアダプターによって受信されます。 この時点で、OID 要求はカプセル化解除し、指定された物理ネットワークアダプターに転送されます。

**注**  Windows Server 2012 以降では、ハードウェアオフロード OID 要求のみがカプセル化され、この方法で転送されます。 たとえば、仮想マシンキュー (VMQ) またはインターネットプロトコルセキュリティ (IPsec) のオフロード OID 要求は、拡張可能なスイッチ制御パスでカプセル化され、転送されます。 詳細については、「[物理ネットワークアダプターに対するハードウェアオフロード OID 要求の管理](managing-hardware-offload-oid-requests-to-physical-network-adapters.md)」を参照してください。

 

<a href="" id="a-forwarding-extension-"></a>転送拡張機能。  
転送拡張機能は、独自のカプセル化された OID 要求を生成し、基になる物理ネットワークアダプターに転送できます。 転送拡張機能は、標準の NDIS OID 要求をカプセル化できます。 また、転送拡張機能は、物理ネットワークアダプター用の独立系ハードウェアベンダー (IHV) によって定義されているプライベート OID 要求をカプセル化することもできます。 これにより、IHV によって開発された転送拡張機能を使用して、チーム内の個々の物理アダプターで独自の属性を有効または無効にすることができます。

また、転送拡張機能は、カプセル化されたハードウェアオフロード OID 要求を送信して、指定した Hyper-v 子パーティションにリソースを割り当てることができます。 たとえば、転送拡張機能は、Oid のカプセル化された OID 要求を受け取ることができます。 [\_受信\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-allocate-queue)を使用して\_キューを割り当て\_、指定した子パーティションに VMQ を割り当てることができます。 この場合、拡張機能は、拡張可能なスイッチポートと、パーティションに関連付けられているネットワークアダプター接続からの要求をカプセル化します。

転送拡張機能は、それまでのドライバーによって発行されたものと同じ OID 要求をフィルター処理している場合にのみ、独自のカプセル化されたハードウェアオフロード OID 要求を発信**する  ます**。 この場合、拡張機能は元の OID 要求を転送することはできません。 代わりに、この要求を完了するために、この拡張機能は[**NdisFOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequestcomplete)を呼び出す必要があります。 NDIS が[*FilterOidRequestComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request_complete)を呼び出して、生成された OID 要求を完了します。

 

<a href="" id="filtering-or-capturing-extensions"></a>拡張機能のフィルター処理またはキャプチャ  
フィルター処理またはキャプチャ拡張機能は、独自のカプセル化された OID クエリ要求を生成し、基になる物理ネットワークアダプターに転送できます。 これらの拡張機能は、物理ネットワークアダプターに対して独立系ハードウェアベンダー (IHV) によって定義されている標準の NDIS OID クエリ要求またはプライベート OID クエリ要求をカプセル化できます。

**注**  転送拡張機能のみが、基になる物理アダプターにカプセル化された OID セット要求を送信することができます。

 

転送拡張機能は、基になる物理アダプターに対してカプセル化された OID 要求を転送、リダイレクト、または発信するときに、次の手順に従う必要があります。

1.  転送拡張機能が OID 要求の発信元である場合は、要求に関連する情報を使用して、拡張機能によって割り当てられた[**NDIS\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体を初期化する必要があります。

    拡張機能が OID 要求を転送する場合、 [*FilterOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request)関数の*OidRequest*パラメーターによって参照される既存の[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造を変更することはできません。 代わりに、拡張機能は[**NdisAllocateCloneOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatecloneoidrequest)を呼び出して新しい**ndis\_oid\_要求**構造にメモリを割り当て、既存の**ndis\_oid\_要求**からすべての情報をコピーする必要があります。データ.

2.  拡張機能によって割り当てられた[**NDIS\_スイッチ\_NIC\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request)構造体のメンバーを次の値に設定します。

    -   **DestinationPortId**メンバーは、外部ネットワークアダプターが接続される拡張可能なスイッチポートの識別子に設定する必要があります。

    -   **DestinationNicIndex**メンバーには、基になる物理ネットワークアダプターの0以外のインデックス値を設定する必要があります。

        これらのインデックス値の詳細については、「[ネットワークアダプターのインデックス値](network-adapter-index-values.md)」を参照してください。

    -   転送拡張機能が Hyper-v 子パーティションに対するハードウェアオフロード OID 要求の発信元である場合、 **SourcePortId**メンバーは、パーティションで使用されるポートの識別子に設定されている必要があります。 また、 **Sourcenicindex**メンバーは、そのポートへのネットワーク接続のネットワークアダプターインデックスに設定されている必要があります。

        転送拡張機能が独自の目的で標準またはプライベートの OID 要求を送信している場合は、 **SourcePortId**と**Sourcenicindex**のメンバーを0に設定する必要があります。

        転送拡張機能がハードウェアオフロード OID 要求を転送またはリダイレクトしている場合は、拡張可能スイッチインターフェイスによって設定された**SourcePortId**および**Sourcenicindex**メンバーの値を保持する必要があります。

    -   **OidRequest**メンバーは、カプセル化された oid 要求の初期化済みの[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造へのポインターに設定する必要があります。 転送拡張機能は、この構造体を割り当てて初期化するか、または構造体の複製されたコピーを使用します。

3.  拡張機能によって割り当てられる[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体のメンバーは、次の値に設定されます。

    -   **Oid**メンバーは、 [\_NIC\_要求に\_スイッチを oid](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)に設定する必要があります。

    -   **Informationbuffer**メンバーには、生成またはフィルター処理された OID 要求データを含むバッファーへのポインターが含まれている必要があります。

    -   **Informationbufferlength**メンバーには、生成またはフィルター処理された OID 要求データを含むバッファーの長さ (バイト単位) が含まれている必要があります。

    拡張機能は、他のメンバーを、 [**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造に対して有効な値に設定します。

4.  この拡張機能は、参照元の物理ネットワークアダプターのインデックスの参照[*カウンターをインクリメントするため*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)に参照を参照します。 これにより、拡張可能なスイッチインターフェイスでは、参照カウンターが0以外の場合に、物理ネットワークアダプターの接続が削除されません。

    拡張機能では[ *、* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic) *SwitchPortId*パラメーターが、 **DestinationPortId**メンバーに対して指定された値に設定されます。 また、この拡張機能は、 *SwitchNicIndex*パラメーターを**DestinationNicIndex**メンバーに指定された値に設定します。

    **注**  は、\_ステータス\_成功しなかっ[*た場合、* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic) OID 要求を宛先物理ネットワークアダプターに転送できません。

     

5.  転送拡張機能が Hyper-v 子パーティションに対してハードウェアオフロード OID 要求を発信している場合は、参照用のファイルを呼び出して、関連付けられているソースネットワークアダプター接続のインデックスの参照[*カウンターをインクリメント*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)します。partition. これにより、拡張可能なスイッチインターフェイスでは、参照カウンターが0以外の場合に、物理ネットワークアダプターの接続が削除されません。

    拡張機能では[ *、* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic) *SwitchPortId*パラメーターが、 **SourcePortId**メンバーに対して指定された値に設定されます。 また、この拡張機能は、 *SwitchNicIndex*パラメーターを**Sourcenicindex**メンバーに指定された値に設定します。

    **注**  は、\_ステータス\_成功しなかっ[*た場合、* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic) OID 要求を宛先物理ネットワークアダプターに転送できません。

     

6.  この拡張機能は、 [**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)を呼び出して、カプセル化された OID 要求を、指定した宛先拡張可能スイッチポートとネットワークアダプターに転送します。

    **注**  フィルター処理された OID 要求を転送する場合は、 [*FilterOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request)関数の呼び出しのコンテキスト内で[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)を呼び出す必要があります。 拡張機能が生成した OID 要求を転送する場合は、*実行*中、*再起動*中、*一時停止*中、*一時停止*中の状態で[**NdisFIndicateStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatestatus)を呼び出します。 これらの状態の詳細については、「[フィルターモジュールの状態と操作](filter-module-states-and-operations.md)」を参照してください。

     

7.  NDIS が[*FilterOidRequestComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request_complete)関数を呼び出すと、拡張機能は[*DereferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_nic)を呼び出して、宛先の物理ネットワークアダプターのインデックスの参照カウンターをクリアします。

    転送拡張機能が Hyper-v 子パーティションに対してハードウェアオフロード OID 要求を発行した場合は、 [*DereferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_nic)を呼び出して、アダプターのソースネットワークアダプター接続のインデックスの参照カウンターをクリアします。

    どちらの場合も、拡張機能は、 *SwitchPortId*パラメーターと*SwitchNicIndex*パラメーターを、の呼び出しで使用したものと同じ値に設定[*します。* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)

拡張機能が OID 要求を発行する方法の詳細については、「 [NDIS フィルタードライバーからの Oid 要求の生成](generating-oid-requests-from-an-ndis-filter-driver.md)」を参照してください。

MUX ドライバーの詳細については、「 [NDIS MUX 中間ドライバー](ndis-mux-intermediate-drivers.md)」を参照してください。

 

 





