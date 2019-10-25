---
title: ネットワーク アダプターでの仮想関数の列挙
description: ネットワーク アダプターでの仮想関数の列挙
ms.assetid: 3AAF2D8B-9C7A-4E5B-86B6-264ACA5EA492
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9777cd2e1a00b5b556064e76cba3f96ccbccb5f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838113"
---
# <a name="enumerating-virtual-functions-on-a-network-adapter"></a>ネットワーク アダプターでの仮想関数の列挙


このドライバーまたはユーザーアプリケーションは、シングルルート i/o 仮想化 (SR-IOV) をサポートするネットワークアダプターのすべての PCI Express (PCIe) 仮想機能 (VFs) の一覧を取得できます。 この一覧を取得するために、ドライバーまたはアプリケーションが[oid\_NIC\_スイッチ\_\_列挙型](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-vfs)のオブジェクト識別子 (oid) メソッド要求を発行します。

ドライバーまたはアプリケーションが OID 要求を発行する前に、要求と共に渡される、 [**VF\_INFO\_配列の構造\_、NDIS\_NIC\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info_array)を初期化する必要があります。 ドライバーまたはアプリケーションは、 **NDIS\_NIC\_スイッチ\_VF\_情報\_配列**構造体を初期化するときに、次のガイドラインに従う必要があります。

-   NDIS\_NIC\_スイッチ\_VF\_情報\_配列\_特定の\_スイッチフラグが**Flags**メンバーで設定されている場合では、前のドライバーまたはアプリケーションが**Switchid**メンバーを sr-iov ネットワークアダプターの NIC スイッチの識別子に設定する必要があります。 これらのメンバーをこのように設定することにより、SR-IOV ネットワークアダプターの指定された NIC スイッチに対してのみ VF 情報が返されます。

    **メモ** その後のドライバーとユーザーモードアプリケーションは、oid\_NIC の OID クエリ要求を発行することによって、NIC スイッチ識別子を取得できます。これにより、[列挙\_スイッチ\_\_スイッチが列挙](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-switches)されます。

-   **Flags**メンバーが0に設定されている場合、ドライバーまたはアプリケーションは**switchid**メンバーを0に設定する必要があります。 この方法でこれらのメンバーを設定することにより、SR-IOV ネットワークアダプターのすべての NIC スイッチに対して VF 情報が返されます。

    **メモ** Windows Server 2012 以降では、ネットワークアダプターの既定の NIC スイッチのみがサポートされます。 **Flags**メンバーで設定されているフラグに関係なく、 **SWITCHID**メンバーを NDIS\_既定\_スイッチ\_ID に設定する必要があります。

この OID クエリ要求から正常に戻った後、 [**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、次を含むバッファーへのポインターが含まれています。

-   [**NDIS\_NIC\_スイッチ\_VF\_INFO\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info_array)配列内の要素の数を定義する配列構造体です。

-   [**VF\_INFO 構造体\_の NDIS\_NIC\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info)の配列。 これらの各構造体には、ネットワークアダプターの NIC スイッチ上の単一の VF に関する情報が含まれています。 VF は、Oid による oid メソッドの要求を介して NIC スイッチに接続されます。 [\_nic\_スイッチによって\_vf が割り当て\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)ます。

    **メモ** ネットワークアダプターの NIC スイッチに VFs が接続されていない場合は、Ndis\_NIC\_スイッチの**Numelements**メンバー [ **\_VF\_INFO\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info_array)構造体はゼロに設定され、 [**NDIS\_NIC\_は切り替わりません。\_VF\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info)構造体が返されます。

    NIC スイッチの詳細については、「 [Nic スイッチ](nic-switches.md)」を参照してください。

NDIS は、ミニポートドライバーの[\_列挙型\_VFS 要求を、OID\_NIC\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-vfs)によって処理します。 NDIS は、次のソースを検査して、管理するデータの内部キャッシュから情報を返します。

-   Oid\_\_スイッチの OID メソッド要求では[\_VF\_割り当てる](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)ことができます。

-   Oid\_\_の oid 設定要求は、 [VF\_パラメーター\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vf-parameters)ます。