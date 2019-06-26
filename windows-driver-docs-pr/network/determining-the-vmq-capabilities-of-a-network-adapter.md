---
title: ネットワーク アダプターの VMQ 機能を判断します。
description: ネットワーク アダプターの VMQ 機能を判断します。
ms.assetid: a8efc393-60fd-4ff8-ba9a-53846f5fbba4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4fa06ce35631fe5e039cc0455027165636764b0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381394"
---
# <a name="determining-the-vmq-capabilities-of-a-network-adapter"></a>ネットワーク アダプターの VMQ 機能を判断します。





NDIS はなど、ネットワーク アダプターの VMQ 機能を決定するインターフェイスを提供します。

-   ネットワーク アダプターの汎用的な機能をフィルター処理します。

-   サポートされている VM のキュー機能。

-   2 つの独立したバッファーに、ネットワーク、メモリ データの分割を許可する先読みをサポートします。

    **注**  NDIS 6.30 以降、パケット データを別の lookahead バッファーに分割することは現在サポートされていません。

     

ミニポート ドライバーでは、ネットワーク アダプターの初期化中に、NDIS に次の情報を提供します。

-   ネットワーク アダプターをサポートできる VMQ ハードウェア機能。

-   現在有効になっている VMQ 機能します。

-   グローバルなネットワーク アダプターを無効または有効にするフィルターの機能が表示されます。

ドライバーとアプリケーションに関連すると、ネットワーク アダプターの機能を取得するのに OID の次のクエリ要求が使用できます。

[OID\_受信\_フィルター\_ハードウェア\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-hardware-capabilities)

[OID\_受信\_フィルター\_現在\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-current-capabilities)

[OID\_RECEIVE\_FILTER\_GLOBAL\_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-global-parameters)

NDIS は、ミニポート ドライバーにこれらの OID クエリ要求を処理します。 そのため、クエリは、ミニポート ドライバーは要求されません。 NDIS は、初期化中に、現在有効になっている受信機能のネットワーク アダプターで VMQ 機能を報告します。 そのため、上にあるドライバーは、これらの Oid をクエリにはありません。

[ **NDIS\_受信\_フィルター\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)構造体は、ネットワーク アダプターのフィルター処理機能を指定します。 この構造体は、次の方法で使用されます。

-   NDIS を呼び出すと、 [ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数、ミニポート ドライバーが初期化することにより、フィルター処理機能を登録、 [ **NDIS\_受信\_フィルター\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)構造体。 ドライバーを設定し、 **HardwareReceiveFilterCapabilities**のメンバー、 [ **NDIS\_ミニポート\_アダプター\_ハードウェア\_ASSIST\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)構造体を指す、 **NDIS\_受信\_フィルター\_機能**構造体。 ドライバーの次の呼び出し、 [ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)関数を設定、 *MiniportAttributes*パラメーターへのポインターを**NDIS\_ミニポート\_アダプター\_ハードウェア\_支援\_属性**構造体。

-   上位のプロトコル ドライバーの受信、 [ **NDIS\_受信\_フィルター\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)構造体、 [ **NDIS\_バインド\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_bind_parameters) NDIS ドライバーを呼び出すときに[ *ProtocolBindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)関数。

-   後続のフィルター ドライバーの受信、 [ **NDIS\_受信\_フィルター\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)構造体、 [ **NDIS\_フィルター\_アタッチ\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_filter_attach_parameters) NDIS ドライバーを呼び出すときに[ *FilterAttach* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_attach)関数。

-   上にあるドライバーが表示される、 [ **NDIS\_ミニポート\_アダプター\_ハードウェア\_支援\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)を発行して構造体クエリ要求を OID を[OID\_受信\_フィルター\_現在\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-current-capabilities)または[OID\_受信\_フィルター\_ハードウェア\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-hardware-capabilities)します。 **HardwareReceiveFilterCapabilities**と**CurrentReceiveFilterCapabilities**メンバーを指す、 [ **NDIS\_受信\_フィルター\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)構造体。

[ **NDIS\_受信\_フィルター\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)構造体には、次の情報が含まれています。

<a href="" id="enabledfiltertypes"></a>**EnabledFilterTypes**  
サポートされている受信フィルターの種類。 NDIS\_受信\_フィルター\_VMQ\_フィルター\_有効フラグは、仮想マシン キュー (VMQ) フィルターが有効になっていることを指定します。

<a href="" id="enabledqueuetypes"></a>**EnabledQueueTypes**  
型がサポートされているキューを受信します。 NDIS\_受信\_フィルター\_VM\_キュー\_有効フラグは、仮想マシン (VM) のキューが有効になっていることを指定します。

<a href="" id="numqueues"></a>**NumQueues**  
ネットワーク アダプターをサポートする受信キューの数。 VMQ をサポートするためにこの数に等しくないか、NIC をサポートするユニキャスト MAC アドレスの数よりも小さいする必要があります。 この数は、既定のキューを含めることはできません。

**注**  ユニキャスト MAC アドレスまたはネットワーク アダプターをサポートする VM のキューの数に関連付けられている NIC の MAC アドレスが含まれません

 

<a href="" id="supportedqueueproperties"></a>**SupportedQueueProperties**  
ネットワーク アダプターをサポートするキューのプロパティ。 NDIS\_受信\_フィルター\_VM\_キュー\_サポートされているフラグは、ネットワーク アダプターが VMQ がフィルター処理をサポートする最小要件を提供することを指定します。 VMQ 対応の NIC は、受信キューごとに、MSI X テーブルのエントリを提供する必要があります。 そのため、VMQ のミニポート ドライバーは、NDIS を設定する必要があります\_受信\_フィルター\_MSI\_X\_サポートされているフラグ。

<a href="" id="supportedfiltertests"></a>**SupportedFilterTests**  
ミニポート ドライバーがサポートするフィルターのテスト操作。 たとえば、ネットワーク アダプターは、指定された値と等しいかどうかを選択したヘッダー フィールドをテストをサポートします。 VMQ のミニポート ドライバーは、NDIS を設定する必要があります\_受信\_フィルター\_テスト\_ヘッダー\_フィールド\_等しい\_サポートされているフラグ。

<a href="" id="supportedheaders"></a>**SupportedHeaders**  
ミニポート ドライバーを検査できるネットワーク パケット ヘッダーの種類。 たとえば、ネットワーク アダプターは、ネットワーク パケットの MAC ヘッダーを検査できます。 MAC ヘッダーには、パケットの種類、変換先およびソース MAC アドレス、VLAN 識別子、および優先順位のタグのフィールドが含まれています。 VMQ のミニポート ドライバーは、NDIS を設定する必要があります\_受信\_フィルター\_MAC\_ヘッダー\_サポートされているフラグ。

<a href="" id="supportedmacheaderfields"></a>**SupportedMacHeaderFields**  
ミニポート ドライバーを検査できる MAC ヘッダー フィールドの種類。 VMQ のミニポート ドライバーは、NDIS を設定する必要があります\_受信\_フィルター\_MAC\_ヘッダー\_DEST\_ADDR\_サポートされているフラグ。

<a href="" id="maxmacheaderfilters"></a>**MaxMacHeaderFilters**  
ミニポート ドライバーがサポートする MAC ヘッダー フィルターの最大数。 少なくとも数のヘッダー フィルター VM キューがある必要があります。

<a href="" id="maxqueuegroups"></a>**MaxQueueGroups**  
このメンバーは、NDIS 用に予約されています。

<a href="" id="maxqueuesperqueuegroup"></a>**MaxQueuesPerQueueGroup**  
このメンバーは、NDIS 用に予約されています。

<a href="" id="minlookaheadsplitsize"></a>**MinLookaheadSplitSize**  
バイト単位の先読みパケットのセグメントのネットワーク アダプターをサポートする最小サイズ。

**注**  NDIS 6.30 以降、パケット データを別の lookahead バッファーに分割することは現在サポートされていません。 NDIS 6.30 以降をサポートするミニポート ドライバーは、このメンバーを 0 に設定する必要があります。

 

<a href="" id="maxlookaheadsplitsize"></a>**MaxLookaheadSplitSize**  
先読みパケットのセグメントのネットワーク アダプターをサポートするには、バイトの最大サイズ。

**注**  NDIS 6.30 以降、パケット データを別の lookahead バッファーに分割することは現在サポートされていません。 NDIS 6.30 以降をサポートするミニポート ドライバーは、このメンバーを 0 に設定する必要があります。

 

正常に戻った後、 [OID\_受信\_フィルター\_ハードウェア\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-hardware-capabilities)OID のクエリ、 **InformationBuffer**のメンバー[ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造には、NDIS へのポインターが含まれる\_受信\_フィルター\_機能の構造体。 これらの機能は、INF ファイルの設定、または、現在無効になっている VMQ ハードウェア機能を含めることができます、**詳細**プロパティ ページ。 VMQ INF の詳細については、設定をファイルを参照してください。 [VMQ の標準的な INF エントリ](https://docs.microsoft.com/windows-hardware/drivers/network/standardized-inf-keywords-for-vmq)します。

NDIS ミニポート ドライバーの初期化中に受信フィルタ リングのハードウェア機能を提供する、 **HardwareReceiveFilterCapabilities**のメンバー、 [ **NDIS\_ミニポート\_アダプター\_ハードウェア\_支援\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)構造体。

正常に戻った後、 [OID\_受信\_フィルター\_現在\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-current-capabilities)OID のクエリ、 **InformationBuffer**のメンバー、[ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体にはへのポインターが含まれています、 [ **NDIS\_受信\_フィルター\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)構造体。 これらの機能には、現在有効になっている VMQ 機能が含まれます。

NDIS ミニポート ドライバーの装置の初期化中にフィルター処理機能が表示される現在有効になっている、 **CurrentReceiveFilterCapabilities**のメンバー、 [ **NDIS\_ミニポート\_アダプター\_ハードウェア\_支援\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)構造体。

NDIS は、現在有効な受信でプロトコル ドライバーに関連する、基になるネットワーク アダプターのフィルター処理機能を報告、 **ReceiveFilterCapabilities**のメンバー、 [ **NDIS\_バインド\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_bind_parameters)バインド操作中に構造体。

[ **NDIS\_受信\_フィルター\_GLOBAL\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_global_parameters)で構造が使用される、 [OID\_受信\_フィルター\_GLOBAL\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-global-parameters)クエリの現在のグローバルを取得する OID がフィルターの設定を受信します。

NDIS\_受信\_フィルター\_GLOBAL\_パラメーターには、次の情報が含まれています。

<a href="" id="enabledfiltertypes"></a>**EnabledFilterTypes**  
有効になっている種類のフィルターを受信します。 NDIS\_受信\_フィルター\_VMQ\_フィルター\_有効フラグは、仮想マシン キュー (VMQ) フィルターが有効になっていることを指定します。

<a href="" id="enabledqueuetypes"></a>**EnabledQueueTypes**  
型が有効になっているキューを受信します。 NDIS\_受信\_フィルター\_VM\_キュー\_有効フラグは、仮想マシン (VM) のキューが有効になっていることを指定します。

正常に戻った後、 [OID\_受信\_フィルター\_GLOBAL\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-global-parameters) OID のクエリ、 **InformationBuffer**のメンバー、[ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体にはへのポインターが含まれています、 [ **NDIS\_受信\_フィルター\_GLOBAL\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_global_parameters)構造体。 NDIS\_受信\_フィルター\_GLOBAL\_パラメーター構造体は、ネットワーク アダプターで有効または無効にする受信フィルタ リング機能を指定します。

NDIS プロトコル ドライバーを使用して、OID\_受信\_フィルター\_GLOBAL\_パラメーターの現在のグローバル構成パラメーターをクエリには、ネットワーク アダプターでフィルター処理を受信します。 プロトコル ドライバーがこの OID を使用して、受信の種類をフィルター処理するかどうかを判断または受信するなど、キューを有効または無効にします。

 

 





