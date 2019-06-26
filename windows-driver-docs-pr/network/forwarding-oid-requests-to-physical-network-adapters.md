---
title: 物理ネットワーク アダプターへの OID 要求の転送
description: 物理ネットワーク アダプターへの OID 要求の転送
ms.assetid: 2A6AA842-FFC2-4CEF-BA56-2FDB277E37C9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fcdbee4fc2cf273f10056b4648edaf0001623de5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382777"
---
# <a name="forwarding-oid-requests-to-physical-network-adapters"></a>物理ネットワーク アダプターへの OID 要求の転送


このトピックでは、HYPER-V 拡張可能スイッチの拡張機能が、HYPER-V 拡張可能スイッチ コントロール パス経由で物理アダプターを基になるオブジェクト識別子 (OID) 要求を転送する方法について説明します。 拡張機能は、このトピックで説明した方法に従って OID 要求は、基になる物理ネットワーク アダプターをも取得できます。

たとえば、外部ネットワーク アダプターは、NDIS マルチプレクサー (マルチプレクサー) の中間ドライバーの仮想ミニポート端にバインドできます。 MUX driver は、ホスト上の 1 つまたは複数の物理ネットワーク チームにバインドされます。 この構成と呼ばれる、*拡張可能スイッチ チーム*します。

この構成で拡張可能スイッチの拡張機能は、チーム内のすべてのネットワーク アダプターに公開されます。 これにより、拡張機能の構成と、チーム内の個々 のネットワーク アダプターの使用を管理できます。 たとえば、転送拡張機能では、個々 のアダプターに送信されるパケットを転送することによって、over、チーム分散フェールオーバー (LBFO) のソリューション ロードのサポートを提供できます。 拡張可能スイッチ チームを管理する転送拡張機能が呼ばれる、*チーミング プロバイダー*します。 プロバイダーのチーミングの詳細については、次を参照してください。[プロバイダーの拡張機能のチーミング](teaming-provider-extensions.md)します。

次の図は、NDIS 6.40 (Windows Server 2012 R2) と後で拡張可能スイッチ チームの例を示します。

![ndis 6.40 の oid コントロール パスの図](images/vswitch-oid-controlpath2-ndis640.png)

次の図は、NDIS 6.30 (Windows Server 2012) の拡張可能スイッチ チームの例を示します。

![ndis 6.30 の拡張可能スイッチ チームのダイアグラム](images/vswitch-oid-controlpath2.png)

**注**  、HYPER-V で拡張可能スイッチのインターフェイス、NDIS フィルターですドライバーがと呼ばれる*拡張可能スイッチの拡張機能*と呼ばれるドライバー スタック、*ドライバー スタックの拡張可能スイッチ。* .

 

OID 要求は、要求を基になる物理ネットワーク アダプターに転送するようにカプセル化する必要があります。 OID 要求はまず内部にカプセル化、 [ **NDIS\_スイッチ\_NIC\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request)構造体。 その後、OID で拡張可能スイッチ コントロールのパス間で転送を要求の OID セット要求によって[OID\_切り替える\_NIC\_要求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)します。

次のように、基になる物理アダプターに OID 要求を発行します。

<a href="" id="the-extensible-switch-interface-"></a>拡張可能スイッチのインターフェイスです。  
OID 要求、ハードウェアの要求の負荷を軽減などを次のいずれかで実行されているプロトコルまたはフィルター ドライバーに関連して発行します。

-   HYPER-V 親パーティションで実行されている管理オペレーティング システム。

-   HYPER-V 子パーティションで実行されているゲスト オペレーティング システム。

拡張可能スイッチで、これらの OID 要求を受信したときにカプセル化されていて、拡張可能スイッチ コントロール パス経由で転送します。 転送拡張機能は、カプセル化された OID 要求を受け取る要求を基になる物理アダプターに転送できます。 この機能は、ハードウェア オフロードの拡張可能スイッチ チームを構成するために特に便利です。

たとえば、MUX driver は、全体の拡張可能スイッチ チームの一般的な機能をアドバタイズします。 ただし、転送拡張機能では、クエリまたはアダプター チーム内の個々 の機能を設定する OID 要求を発行できます。 次に、転送拡張機能では、チーム全体に適用される機能の詳細の上にあるドライバーに通知する外部ネットワーク アダプターから NDIS 状態を示す値を取得できます。 この手順の詳細については、次を参照してください。 [NDIS 状態インジケーターの元の物理ネットワーク アダプターから](originating-ndis-status-indications-from-physical-network-adapters.md)します。

転送拡張機能は、コントロールのパス経由で OID 要求を転送するとき、外部のネットワーク アダプターで受信します。 この時点で、OID 要求では、カプセル化解除されたがあり、指定した物理ネットワーク アダプターに転送します。

**注**  ハードウェア オフロード OID のみ、Windows Server 2012 以降の要求をカプセル化し、この方法で転送します。 たとえば、仮想マシン キュー (VMQ) の OID 要求の負荷を軽減またはインターネット プロトコル セキュリティ (IPsec) をカプセル化され、拡張可能スイッチ コントロール パス経由で転送します。 詳細については、次を参照してください。[を管理するハードウェア オフロード OID 要求を物理ネットワーク アダプター](managing-hardware-offload-oid-requests-to-physical-network-adapters.md)します。

 

<a href="" id="a-forwarding-extension-"></a>転送拡張機能。  
転送拡張機能では、独自のカプセル化された OID 要求を送信でき、それらを基になる物理ネットワーク アダプターに転送することができます。 転送拡張機能には、標準の NDIS OID 要求がカプセル化できます。 転送拡張機能は、物理ネットワーク アダプターの独立系ハードウェア ベンダー (IHV) で定義されているプライベートの OID 要求をカプセル化もできます。 これにより、IHV 有効または、チーム内の個々 の物理アダプターに専用の属性を無効にして開発されたも転送拡張機能です。

さらに、転送拡張機能では、指定された HYPER-V 子パーティションのリソースの割り当てをカプセル化されたハードウェア オフロード OID 要求を取得できます。 たとえば、転送拡張機能はのカプセル化された OID 要求発信元[OID\_受信\_フィルター\_ALLOCATE\_キュー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-allocate-queue)指定子を VMQ を割り当てられませんパーティション。 この場合、拡張機能には、パーティションに関連付けられている拡張可能スイッチ ポートとネットワーク アダプター接続からのもので、要求がカプセル化します。

**注**  重なってドライバーによって発行された同じ OID 要求のフィルタ リングは、その場合、転送拡張機能は独自のカプセル化されたハードウェア オフロード OID 要求を発信のみことができます。 ここでは、拡張する必要があります、OID の元の要求を転送しません。 代わりに、拡張機能を呼び出す必要があります[ **NdisFOidRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequestcomplete) NDIS を呼び出すと、この要求を完了するその[ *FilterOidRequestComplete* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_oid_request_complete)から配信された OID 要求を完了します。

 

<a href="" id="filtering-or-capturing-extensions"></a>フィルター処理や拡張機能のキャプチャ  
フィルター処理や拡張機能のキャプチャは、独自のカプセル化された OID クエリ要求を発信し、それらを基になる物理ネットワーク アダプターに転送できます。 これらの拡張機能は、標準の NDIS OID クエリが物理ネットワーク アダプターの独立系ハードウェア ベンダー (IHV) で定義されている要求のクエリ要求またはプライベートの OID をカプセル化できます。

**注**  転送拡張機能と、基になる物理アダプターにカプセル化された OID セットの要求が発生することだけです。

 

転送をリダイレクトする、または基になる物理アダプターのカプセル化された、OID 要求の発生元、転送拡張機能は次の手順に従う必要があります。

1.  拡張機能の割り当てが初期化する必要がある場合は、転送拡張機能が、OID 要求を発信、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)に関連する情報を含む構造体要求。

    場合、拡張機能では、OID、要求の転送にする必要がありますは変わりません既存[ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)によって参照される構造体、 *OidRequest*のパラメーター、 [ *FilterOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_oid_request)関数。 代わりに、拡張機能を呼び出す必要があります[ **NdisAllocateCloneOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatecloneoidrequest)を新しいメモリを割り当てる**NDIS\_OID\_要求**構造と既存のすべての情報をコピー **NDIS\_OID\_要求**構造体。

2.  拡張機能設定の拡張機能が割り当てたメンバー [ **NDIS\_スイッチ\_NIC\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request)構造体を次の値。

    -   **DestinationPortId**メンバーは、外部ネットワーク アダプターが接続されている拡張可能スイッチ ポートの識別子を設定する必要があります。

    -   **DestinationNicIndex**メンバーは、基になる物理ネットワーク アダプターの 0 以外のインデックス値に設定する必要があります。

        これらのインデックス値の詳細については、次を参照してください。[ネットワーク アダプターのインデックス値](network-adapter-index-values.md)します。

    -   転送拡張機能が HYPER-V 子パーティションでは、ハードウェアのオフロード OID 要求を発信する場合、 **SourcePortId**メンバーは、パーティションによって使用されるポートの識別子を設定する必要があります。 また、 **SourceNicIndex**メンバーは、そのポートへのネットワーク接続のネットワーク アダプターのインデックスを設定する必要があります。

        転送拡張機能が、独自の目的で、標準またはプライベートの OID 要求を発信する場合、 **SourcePortId**と**SourceNicIndex**メンバーは 0 に設定する必要があります。

        値を保持する必要がある場合、転送拡張機能を転送、またはハードウェア オフロード OID 要求をリダイレクトする場合、 **SourcePortId**と**SourceNicIndex**拡張可能なによって設定されたメンバースイッチのインターフェイスです。

    -   **OidRequest**メンバーが初期化されたへのポインターを設定する必要があります[ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)カプセル化された OID 要求の構造. 転送拡張機能を割り当てますこの構造体を初期化しますか、構造体の複製コピーを使用します。

3.  拡張機能設定の拡張機能が割り当てたメンバー [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体を次の値。

    -   **Oid**にメンバーを設定する必要があります[OID\_スイッチ\_NIC\_要求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)します。

    -   **InformationBuffer**メンバーは、生成されたまたはフィルター選択された OID 要求データを格納しているバッファーへのポインターを含める必要があります。

    -   **InformationBufferLength**メンバーは、生成されたまたはフィルター選択された OID 要求データを格納しているバッファーの長さ、(バイト単位) を含める必要があります。

    拡張機能が有効な値に他のメンバーを設定、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体。

4.  拡張機能の呼び出し[ *ReferenceSwitchNic* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_reference_switch_nic)を変換先の物理ネットワーク アダプターのインデックスの参照カウンターをインクリメントします。 これにより、エントリの中に、その参照カウンターが 0 以外の場合、拡張可能スイッチのインターフェイスは物理ネットワーク アダプターの接続が削除されません。

    拡張機能を呼び出すと[ *ReferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_reference_switch_nic)、設定、 *SwitchPortId*パラメーターに指定された値を**DestinationPortId**メンバー。 また、拡張機能、設定、 *SwitchNicIndex*パラメーターに指定された値を**DestinationNicIndex**メンバー。

    **注**  場合[ *ReferenceSwitchNic* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_reference_switch_nic) NDIS を返さない\_状態\_成功すると、OID 要求は、宛先に転送することはできません物理ネットワーク アダプター。

     

5.  呼び出す場合、転送拡張機能には、HYPER-V 子パーティションのハードウェアのオフロード OID 要求が送信された、 [ *ReferenceSwitchNic* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_reference_switch_nic)ソースのインデックスの参照カウンターをインクリメントするにはパーティションに関連付けられているネットワーク アダプターの接続。 これにより、エントリの中に、その参照カウンターが 0 以外の場合、拡張可能スイッチのインターフェイスは物理ネットワーク アダプターの接続が削除されません。

    拡張機能を呼び出すと[ *ReferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_reference_switch_nic)、設定、 *SwitchPortId*パラメーターに指定された値を**SourcePortId**メンバー。 また、拡張機能、設定、 *SwitchNicIndex*パラメーターに指定された値を**SourceNicIndex**メンバー。

    **注**  場合[ *ReferenceSwitchNic* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_reference_switch_nic) NDIS を返さない\_状態\_成功すると、OID 要求は、宛先に転送することはできません物理ネットワーク アダプター。

     

6.  拡張機能の呼び出し[ **NdisFOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequest)カプセル化された OID 要求を指定したコピー先の拡張可能スイッチ ポートとネットワーク アダプターに転送するようにします。

    **注**  呼び出す必要がありますが、拡張機能では、フィルター選択された OID 要求の転送する場合[ **NdisFOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequest)への呼び出しのコンテキスト内でその[ *FilterOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_oid_request)関数。 場合、拡張機能が生成された OID 要求、転送呼び出し[ **NdisFIndicateStatus** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfindicatestatus)になっている、*を実行している*、 *を再開しています*、 *Paused*、および*一時停止中*状態。 これらの状態の詳細については、次を参照してください。[フィルター モジュールの状態と操作](filter-module-states-and-operations.md)します。

     

7.  NDIS を呼び出すと、 [ *FilterOidRequestComplete* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_oid_request_complete)関数では、拡張機能の呼び出し[ *DereferenceSwitchNic* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_dereference_switch_nic)をオフにします変換先の物理ネットワーク アダプターのインデックスの参照カウンターです。

    呼び出す場合、転送拡張機能には、HYPER-V 子パーティションのハードウェアのオフロード OID 要求が発生した、 [ *DereferenceSwitchNic* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_dereference_switch_nic)ソースのインデックスの参照カウンターをクリアするにはアダプターのネットワーク アダプターの接続。

    どちらの場合で、拡張機能の設定、 *SwitchPortId*と*SwitchNicIndex*を同じパラメーター値への呼び出しで使用されるその it [ *ReferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_reference_switch_nic).

拡張機能が OID 要求を発行する方法の詳細については、次を参照してください。 [NDIS フィルター ドライバーから OID の要求を生成する](generating-oid-requests-from-an-ndis-filter-driver.md)します。

MUX ドライバーの詳細については、次を参照してください。 [NDIS MUX 中間ドライバー](ndis-mux-intermediate-drivers.md)します。

 

 





