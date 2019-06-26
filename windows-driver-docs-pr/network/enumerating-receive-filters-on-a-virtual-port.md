---
title: 仮想ポートでの受信フィルターの列挙
description: 仮想ポートでの受信フィルターの列挙
ms.assetid: E809B7A3-256B-4351-8A60-D80D4A86EFDB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18d63f98b33e1e201b12dc0f98a1a014865dfc5c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354563"
---
# <a name="enumerating-receive-filters-on-a-virtual-port"></a>仮想ポートでの受信フィルターの列挙





仮想ポート (VPort) で作成した後は、スイッチ、NIC のネットワーク アダプター、上にあるドライバーとユーザー アプリケーションは、次に実行できます。

-   受信フィルターを VPort のパラメーターを列挙します。

    詳細については、次を参照してください。[受信フィルターを列挙する](#enumerating-receive-filters)します。

-   特定の受信のフィルターのパラメーターをクエリします。

    詳細については、次を参照してください。[特定の受信のフィルターのクエリを実行する](#querying-a-specific-receive-filter)します。

VPort を作成する方法の詳細については、次を参照してください。[仮想ポートを作成する](creating-a-virtual-port.md)します。

## <a name="enumerating-receive-filters"></a>受信フィルターを列挙


一覧を取得するフィルター ドライバーが重なって、NIC のスイッチの仮想ポート (VPort) に設定されているすべての受信し、アプリケーションは要求を発行オブジェクト識別子 (OID) メソッドの[OID\_受信\_フィルター\_列挙型\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)します。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体は、初期状態へのポインターを含む、 [**NDIS\_受信\_フィルター\_情報\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)構造体。

上にあるドライバーまたはユーザーのアプリケーションでは、この OID メソッド要求を発行、前に初期化する必要があります、 [ **NDIS\_受信\_フィルター\_情報\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)構造体し、次のように、この構造体のメンバーを設定します。

-   **QueueId** NDIS にメンバーを設定する必要があります\_既定\_受信\_キュー\_id。

-   **VPortId** VPort に関連付けられている識別子にメンバーを設定する必要があります。 上にあるドライバーは、次の方法のいずれかで VPort 識別子を取得します。

    -   前の OID メソッド要求から[OID\_NIC\_スイッチ\_作成\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)します。

    -   前の OID メソッド要求から[OID\_NIC\_スイッチ\_ENUM\_拡張](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-vports)します。

    **注**  このメンバーは有効の場合は、ドライバーまたはアプリケーションの設定、NDIS のみ\_受信\_フィルター\_情報\_配列\_VPORT\_ID\_で指定されたフラグ、**フラグ**メンバー。 このフラグが設定されていない場合は、受信すべて VPort NIC スイッチ上で設定されたフィルターが返されます。

     

OID メソッド要求から正常に戻った後[OID\_受信\_フィルター\_ENUM\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)、 **InformationBuffer**のメンバー[ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造には、更新されたへのポインターが含まれる[ **NDIS\_受信\_フィルター\_情報\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)構造体が 1 つまたは複数続く[ **NDIS\_受信\_フィルター\_情報** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_info)構造体。 各**NDIS\_受信\_フィルター\_情報**構造体を指定した VPort が設定されている受信フィルターの一意の識別子を指定します。

## <a name="querying-a-specific-receive-filter"></a>特定の受信のフィルターのクエリを実行します。


ドライバーやアプリケーションの後続の OID メソッド要求を発行できます[OID\_受信\_フィルター\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-parameters) VPort の特定のフィルターのパラメーターを取得します。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体は、初期状態へのポインターを含む、 [**NDIS\_受信\_フィルター\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)構造体。

上にあるドライバーまたはユーザーのアプリケーションでは、この OID メソッド要求を発行、前に初期化する必要があります、 [ **NDIS\_受信\_フィルター\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)構造化し、次のようにこの構造体のメンバーを設定します。

-   **FilterId**メンバーは、パラメーターが返されるフィルターの 0 以外の id の値に設定する必要があります。

    **注**  上にあるドライバーから以前の OID メソッド要求のフィルターの識別子を取得した[OID\_受信\_フィルター\_設定\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)または[OID\_受信\_フィルター\_ENUM\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)します。 アプリケーションは、OID の以前の OID メソッド要求からのみ、フィルターの識別子を取得できます\_受信\_フィルター\_ENUM\_フィルター。

     

-   **QueueId** NDIS にメンバーを設定する必要があります\_既定\_受信\_キュー\_id。

-   **VPortId** VPort に関連付けられている識別子にメンバーを設定する必要があります。 上にあるドライバーは、次の方法のいずれかで VPort 識別子を取得します。

    -   前の OID メソッド要求から[OID\_NIC\_スイッチ\_作成\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)します。

    -   前の OID メソッド要求から[OID\_NIC\_スイッチ\_ENUM\_拡張](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-vports)します。

NDIS ハンドル、 [OID\_受信\_フィルター\_ENUM\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)と[OID\_受信\_フィルター\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-parameters)メソッド OID は、ミニポート ドライバーを要求します。 NDIS から受信したデータの内部キャッシュからの情報の取得、 [OID\_受信\_フィルター\_設定\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter) OID 要求。

 

 





