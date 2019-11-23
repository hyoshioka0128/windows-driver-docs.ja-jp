---
title: 仮想ポートでの受信フィルターの列挙
description: 仮想ポートでの受信フィルターの列挙
ms.assetid: E809B7A3-256B-4351-8A60-D80D4A86EFDB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd84666d51a6e20825eef721be1c165a4cdcbb9d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838117"
---
# <a name="enumerating-receive-filters-on-a-virtual-port"></a>仮想ポートでの受信フィルターの列挙





ネットワークアダプターの NIC スイッチに仮想ポート (VPort) が作成されると、その後のドライバーとユーザーアプリケーションは次のことができるようになります。

-   VPort で受信フィルターのパラメーターを列挙します。

    詳細については、「[受信フィルターの列挙](#enumerating-receive-filters)」を参照してください。

-   特定の受信フィルターのパラメーターに対してクエリを実行します。

    詳細については、「[特定の受信フィルターのクエリ](#querying-a-specific-receive-filter)」を参照してください。

VPort の作成方法の詳細については、「[仮想ポートの作成](creating-a-virtual-port.md)」を参照してください。

## <a name="enumerating-receive-filters"></a>受信フィルターの列挙


NIC スイッチの仮想ポート (VPort) に設定されているすべての受信フィルターの一覧を取得するには、その後のドライバーとアプリケーションが Oid のオブジェクト識別子 (OID) メソッド要求を発行[\_、列挙\_フィルター\_列挙\_フィルターを受け取る](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)ことができます。

[**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、最初に、 [ **\_フィルター\_情報\_配列構造を受け取る ndis\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)を指すポインターが含まれています。

この OID メソッド要求を実行する前に、この OID メソッドの要求を発行する前に、次のように[ **\_フィルター\_情報\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)の構造を受け取って、この構造体のメンバーを設定するために、NDIS を初期化\_必要があります。

-   **Queueid**メンバーを NDIS\_既定\_受信\_キュー\_ID に設定する必要があります。

-   **VPortId**メンバーは、vport に関連付けられた識別子に設定する必要があります。 このドライバーは、次のいずれかの方法で VPort 識別子を取得します。

    -   Oid\_の以前の OID メソッド要求から、 [\_VPORT を作成\_\_スイッチに切り替え](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)ます。

    -   Oid\_NIC の以前の OID メソッド要求から、[列挙型\_VPORTS\_スイッチ\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-vports)ます。

    このメンバーが有効になるのは、ドライバーまたはアプリケーションによって NDIS\_受信\_フィルター\_情報\_配列\_VPORT\_ID\_**フラグ**メンバーの指定されたフラグが設定されている場合**のみ  ます**。 このフラグが設定されていない場合、NIC スイッチのすべての VPort に設定された受信フィルターが返されます。

     

Oid の OID メソッド要求から正常に返された後[\_フィルター\_列挙\_フィルターを受け取る\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)、 [**ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、更新された NDIS [ **\_receive\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info) [**filter\_info\_ARRAY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)構造体へのポインターが含まれます。\_\_\_ 各**NDIS\_受信\_フィルター\_情報**構造は、指定された vport に設定されている受信フィルターの一意の識別子を指定します。

## <a name="querying-a-specific-receive-filter"></a>特定の受信フィルターのクエリ


それ以降のドライバーまたはアプリケーションでは、oid の OID メソッド要求を発行して、VPort の特定のフィルターのパラメーターを取得[\_フィルター\_パラメーターを受け取る\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-parameters)できます。

[**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、最初は[**ndis\_RECEIVE\_FILTER\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)構造体へのポインターが含まれています。

この OID メソッドの要求を実行する前に、この OID メソッドの要求を発行する前に、次の方法でこの構造体のメンバーを設定するために、NDIS を初期化する必要があります。この場合、 [ **\_フィルター\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)構造を\_してください。

-   **Filterid**メンバーは、パラメーターが返されるフィルターの0以外の識別子の値に設定する必要があります。

    これまでのドライバーでは、以前の OID メソッドの Oid 要求からフィルター識別子を取得した  [\_受信\_フィルター\_設定さ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)れている**ことに注意**してください\_フィルター\_列挙\_フィルター\_列挙\_フィルター[列挙](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)します。 アプリケーションでフィルター識別子を取得できるのは、以前の oid メソッドの OID の要求からだけで、列挙\_フィルター\_列挙型の\_フィルターを受け取る\_です。

     

-   **Queueid**メンバーを NDIS\_既定\_受信\_キュー\_ID に設定する必要があります。

-   **VPortId**メンバーは、vport に関連付けられた識別子に設定する必要があります。 このドライバーは、次のいずれかの方法で VPort 識別子を取得します。

    -   Oid\_の以前の OID メソッド要求から、 [\_VPORT を作成\_\_スイッチに切り替え](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)ます。

    -   Oid\_NIC の以前の OID メソッド要求から、[列挙型\_VPORTS\_スイッチ\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-vports)ます。

NDIS は、 [\_フィルター\_列挙型\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)フィルターおよび OID を受け取る oid\_、ミニポートドライバーに対して\_パラメーターメソッド oid 要求を[受信\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-parameters)処理します。\_ NDIS は、oid から受信したデータの内部キャッシュから情報を取得し、 [\_フィルター\_設定](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)して oid 要求\_フィルター処理\_ます。

 

 





