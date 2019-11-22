---
title: ネットワークアダプターの VMQ 機能の決定
description: ネットワークアダプターの VMQ 機能の決定
ms.assetid: a8efc393-60fd-4ff8-ba9a-53846f5fbba4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc349c4f8e011e78ad9f9cb2649a66a5af186c7d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834897"
---
# <a name="determining-the-vmq-capabilities-of-a-network-adapter"></a>ネットワークアダプターの VMQ 機能の決定





NDIS には、ネットワークアダプターの VMQ 機能を決定するインターフェイスが用意されています。次に例を示します。

-   ネットワークアダプターの汎用的なフィルター処理機能。

-   サポートされている VM キュー機能。

-   先読みサポートにより、ネットワークデータメモリを2つの異なるバッファーに分割できるようになります。

    **注**  NDIS 6.30 以降では、パケットデータを個別の先読みバッファーに分割することはサポートされなくなりました。

     

ミニポートドライバーは、ネットワークアダプターの初期化中に次の情報を NDIS に提供します。

-   ネットワークアダプターがサポートできる VMQ ハードウェア機能。

-   現在有効になっている VMQ 機能。

-   ネットワークアダプターで有効または無効にされているグローバル受信フィルター機能。

その後のドライバーとアプリケーションは、次の OID クエリ要求を使用して、ネットワークアダプターの機能を取得できます。

[OID\_ハードウェア\_機能\_\_フィルターを受け取る](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-hardware-capabilities)

[OID\_現在の\_機能\_受信\_フィルター処理](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-current-capabilities)

[グローバル\_パラメーター\_\_フィルターを受け取る OID\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-global-parameters)

NDIS は、ミニポートドライバーに対するこれらの OID クエリ要求を処理します。 そのため、このクエリはミニポートドライバーには要求されません。 NDIS は、初期化中に、ネットワークアダプターの現在有効な受信 VMQ 機能を報告します。 そのため、それ以上のドライバーでは、これらの Oid に対してクエリを実行する必要はありません。

[**NDIS\_RECEIVE\_FILTER\_capabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)構造体は、ネットワークアダプターのフィルター機能を指定します。 この構造体は、次の方法で使用されます。

-   NDIS が[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数を呼び出すと、ミニポートドライバーは、\_ndis を初期化することによってフィルター機能を登録し、 [ **\_フィルター\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)構造を受信します。 次に、ドライバーは[**ndis\_ミニポート\_\_アダプター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)の**HardwareReceiveFilterCapabilities**メンバーを設定し、\_属性構造を提供して ndis\_RECEIVE をポイントするように\_支援 **\_\_機能**の構造をフィルター処理します。 次に、ドライバーは[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)関数を呼び出した後、 *miniportattributes*パラメーターを NDIS\_ミニポート\_アダプターへのポインターに設定します **\_ハードウェア\_支援\_属性**構造体。

-   プロトコルドライバーは ndis [ **\_受信\_フィルター\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)の構造を受け取り、ndis\_がドライバーの[*Protocolbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)を呼び出したときに、 [ **\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)構造をバインドします。プロシージャ.

-   前のフィルタードライバーは ndis [ **\_受信\_フィルター\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)の\_構造を受け取り、ndis がドライバーの[*filterattach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)関数を呼び出したときに[ **\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters)構造をアタッチ\_ます。

-   これまでのドライバーでは、 [**NDIS\_ミニポート\_アダプター\_ハードウェア\_\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)の構造を受け取るために、OID の oid クエリ要求を発行することによって\_\_を受信\_[フィルター\_現在機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-current-capabilities)または[OID\_\_フィルター\_ハードウェア\_機能を受信](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-hardware-capabilities)します。 **HardwareReceiveFilterCapabilities**および**currentreceivefiltercapabilities**メンバーは、 [**NDIS\_受信\_フィルター\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)の構造を指します。

[**NDIS\_受信\_フィルター\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)の構造には、次の情報が含まれています。

<a href="" id="enabledfiltertypes"></a>**EnabledFilterTypes**  
サポートされている受信フィルターの種類。 [NDIS\_RECEIVE\_FILTER\_VMQ\_FILTERS]\_ENABLED フラグは、バーチャルマシンキュー (VMQ) フィルターが有効であることを指定します。

<a href="" id="enabledqueuetypes"></a>**EnabledQueueTypes**  
サポートされている受信キューの種類。 NDIS\_RECEIVE\_FILTER\_VM\_QUEUE\_ENABLED フラグは、仮想マシン (VM) キューが有効であることを指定します。

<a href="" id="numqueues"></a>**NumQueues**  
ネットワークアダプターがサポートする受信キューの数。 VMQ をサポートするには、NIC がサポートしているユニキャスト MAC アドレスの数と同じかそれより小さい値を指定する必要があります。 この数には、既定のキューを含めないでください。

ネットワークアダプターがサポートしているユニキャスト MAC アドレスまたは VM キューの数には、関連付けられている NIC の MAC アドレスが含まれていないことに**注意**してください  。

 

<a href="" id="supportedqueueproperties"></a>**SupportedQueueProperties**  
ネットワークアダプターがサポートするキュープロパティ。 NDIS\_RECEIVE\_FILTER\_VM\_QUEUE\_supported フラグは、ネットワークアダプターが VMQ フィルターをサポートするための最小要件を提供することを指定します。 VMQ 対応の NIC は、各受信キューに対して MSI-X テーブルエントリを提供する必要があります。 したがって、VMQ ミニポートドライバーでは、NDIS\_RECEIVE\_FILTER\_MSI\_X\_supported フラグが設定されている必要があります。

<a href="" id="supportedfiltertests"></a>**SupportedFilterTests**  
ミニポートドライバーがサポートするフィルターテスト操作。 たとえば、ネットワークアダプターは、選択されたヘッダーフィールドのテストをサポートして、指定された値と等しいかどうかを判断します。 VMQ ミニポートドライバーでは、NDIS\_RECEIVE\_FILTER\_TEST\_HEADER\_FIELD\_supported\_supported フラグが設定されている必要があります。

<a href="" id="supportedheaders"></a>**SupportedHeaders**  
ミニポートドライバーが検査できるネットワークパケットヘッダーの種類。 たとえば、ネットワークアダプターはネットワークパケットの MAC ヘッダーを調べることができます。 MAC ヘッダーには、パケットの種類、宛先とソースの MAC アドレス、VLAN 識別子、および優先度タグのフィールドが含まれています。 VMQ ミニポートドライバーでは、NDIS\_RECEIVE\_FILTER\_MAC\_HEADER\_supported フラグが設定されている必要があります。

<a href="" id="supportedmacheaderfields"></a>**SupportedMacHeaderFields**  
ミニポートドライバーが調べることができる MAC ヘッダーフィールドの種類。 VMQ ミニポートドライバーでは、NDIS\_受信\_フィルター\_MAC\_ヘッダー\_DEST\_ADDR\_サポートされているフラグを設定する必要があります。

<a href="" id="maxmacheaderfilters"></a>**MaxMacHeaderFilters**  
ミニポートドライバーがサポートする MAC ヘッダーフィルターの最大数。 少なくとも1つのヘッダーフィルターが VM キューの数と同じである必要があります。

<a href="" id="maxqueuegroups"></a>**MaxQueueGroups**  
このメンバーは NDIS 用に予約されています。

<a href="" id="maxqueuesperqueuegroup"></a>**MaxQueuesPerQueueGroup**  
このメンバーは NDIS 用に予約されています。

<a href="" id="minlookaheadsplitsize"></a>**Minfeel Splitsize**  
ネットワークアダプターが先読みパケットセグメントに対してサポートする最小サイズ (バイト単位)。

**注**  NDIS 6.30 以降では、パケットデータを個別の先読みバッファーに分割することはサポートされなくなりました。 NDIS 6.30 以降のバージョンをサポートするミニポートドライバーでは、このメンバーを0に設定する必要があります。

 

<a href="" id="maxlookaheadsplitsize"></a>**Maxlook Aヘッド Splitsize**  
ネットワークアダプターが先読みパケットセグメントに対してサポートする最大サイズ (バイト単位)。

**注**  NDIS 6.30 以降では、パケットデータを個別の先読みバッファーに分割することはサポートされなくなりました。 NDIS 6.30 以降のバージョンをサポートするミニポートドライバーでは、このメンバーを0に設定する必要があります。

 

Oid から正常に返された後[\_フィルター\_ハードウェア\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-hardware-capabilities)の oid クエリを受け取る\_、 [**NDIS\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーにはポインターが含まれていますNDIS\_\_フィルター\_機能の構造を受け取ることができます。 これらの機能には、現在 INF ファイル設定で無効になっている VMQ ハードウェア機能や、 **[詳細設定**] プロパティページがあります。 VMQ の INF ファイルの設定の詳細については、「 [Vmq STANDARD Inf Entries](https://docs.microsoft.com/windows-hardware/drivers/network/standardized-inf-keywords-for-vmq)」を参照してください。

NDIS ミニポートドライバーは、Ndis\_ミニポート\_アダプターの**HardwareReceiveFilterCapabilities**メンバーである初期化中に、受信フィルターのハードウェア機能を提供し[ **\_ハードウェア\_支援\_ATTRIBUTES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)構造体。

Oid から正常に返された後[\_フィルター\_現在の\_機能の](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-current-capabilities)oid クエリを受け取る\_、 [**NDIS\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーにはポインターが含まれています[**NDIS\_\_フィルター\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)の構造を受け取ることができます。 これらの機能には、現在有効になっている VMQ 機能が含まれます。

NDIS ミニポートドライバーは、Ndis\_ミニポート\_アダプター\_ハードウェア\_アシストの**Currentreceivefiltercapabilities**メンバーでの初期化中に、現在有効になっている受信フィルター機能を提供[ **@no__ 属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)構造体。\_

NDIS は、バインド操作中に、基になるネットワークアダプターの現在有効に**なっている**受信フィルター機能を、 [**ndis\_bind\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)構造内のプロトコルドライバーに報告します。

[ **\_フィルター\_グローバル\_パラメーターの構造を受け取る NDIS\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_global_parameters)は、グローバル[\_パラメーターを受信\_フィルター\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-global-parameters) 、現在のグローバル受信フィルターを取得するために、oid で使用されます。設定。\_

NDIS\_は、グローバル\_パラメーター\_\_フィルターを受け取ると、次の情報が含まれます。

<a href="" id="enabledfiltertypes"></a>**EnabledFilterTypes**  
有効な受信フィルターの種類。 [NDIS\_RECEIVE\_FILTER\_VMQ\_FILTERS]\_ENABLED フラグは、バーチャルマシンキュー (VMQ) フィルターが有効であることを指定します。

<a href="" id="enabledqueuetypes"></a>**EnabledQueueTypes**  
有効な受信キューの種類。 NDIS\_RECEIVE\_FILTER\_VM\_QUEUE\_ENABLED フラグは、仮想マシン (VM) キューが有効であることを指定します。

Oid から正常に返された後、[グローバル\_パラメーターの\_を受け取る\_フィルターを受け取る](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-global-parameters)oid クエリ\_、 [**NDIS\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、[**NDIS\_は、グローバル\_パラメーター構造\_\_フィルターを受信**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_global_parameters)します。 NDIS\_RECEIVE\_FILTER\_GLOBAL\_PARAMETERS 構造体は、ネットワークアダプターで有効または無効になっている受信フィルター機能を指定します。

NDIS プロトコルドライバーは、OID\_使用して、グローバル\_パラメーター\_受信\_フィルター処理し、ネットワークアダプターの受信フィルター処理のために現在のグローバル構成パラメーターを照会します。 たとえば、プロトコルドライバーは、この OID を使用して、受信フィルターの種類または受信キューを有効にするか無効にするかを決定できます。

 

 





