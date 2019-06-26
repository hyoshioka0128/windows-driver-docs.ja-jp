---
title: ネットワーク アダプターでの仮想ポートの列挙
description: ネットワーク アダプターでの仮想ポートの列挙
ms.assetid: 437C3356-4CC7-4128-9E61-FD01157F4FD9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9106f265c4957857be6b90490fb15a5c9e2a04fc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384560"
---
# <a name="enumerating-virtual-ports-on-a-network-adapter"></a>ネットワーク アダプターでの仮想ポートの列挙


上にあるドライバーまたはユーザーのアプリケーションは、シングル ルート I/O 仮想化 (SR-IOV) をサポートするネットワーク アダプターの NIC のスイッチ上のすべての仮想ポート (拡張) の一覧を取得できます。 ドライバーまたはアプリケーションのオブジェクト識別子 (OID) メソッド要求を発行[OID\_NIC\_スイッチ\_ENUM\_拡張](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-vports)この一覧を取得します。

この OID クエリ要求から正常に戻った後、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体以下を含むバッファーへのポインターが含まれます。

-   [ **NDIS\_NIC\_スイッチ\_VPORT\_情報\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_info_array)配列内の要素の数を定義する構造体。

-   配列の[ **NDIS\_NIC\_スイッチ\_VPORT\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_info)構造体。 各構造体には、ネットワーク アダプターの NIC のスイッチ上の VPort に関する情報が含まれています。

    **注**  ネットワーク アダプターの拡張が作成されていない場合、ドライバーの設定、 **NumElements**のメンバー、 [ **NDIS\_NIC\_スイッチ\_VPORT\_情報\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_info_array)構造体を 0、no [ **NDIS\_NIC\_スイッチ\_VPORT\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_info)構造体が返されます。

     

上にあるドライバーやユーザー アプリケーションの問題の前に、 [OID\_NIC\_スイッチ\_ENUM\_拡張](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-vports)要求と、それを初期化する必要があります、 [ **NDIS\_NIC\_スイッチ\_VPORT\_情報\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_info_array)要求と共に渡される構造体。 ドライバーまたはアプリケーションは、初期化するときに、次のガイドラインに従う必要があります、 **NDIS\_NIC\_スイッチ\_VPORT\_情報\_配列**構造体。

-   場合は、NDIS\_NIC\_スイッチ\_VPORT\_情報\_配列\_ENUM\_ON\_特定\_スイッチ フラグに設定されて、 **フラグ**メンバー、指定した NIC のスイッチで作成されたすべての拡張の情報が返されます。 NIC のスイッチがで指定された、 **SwitchId**その構造体のメンバー。

    **注**  以降 Windows Server 2012 では、SR-IOV インターフェイスをサポートしています NIC スイッチが 1 つだけ、ネットワーク アダプター。 このスイッチと呼ばれる、 *NIC スイッチの既定*、NDIS によって参照されている\_既定\_スイッチ\_ID です。 設定されているフラグに関係なく、**フラグ**、メンバー、 **SwitchId** NDIS にメンバーを設定する必要があります\_既定\_スイッチ\_id。

     

-   場合は、NDIS\_NIC\_スイッチ\_VPORT\_情報\_配列\_ENUM\_ON\_特定\_関数フラグに設定されて、 **フラグ**メンバー、ネットワーク アダプターで指定された PCI Express (PCIe) 物理機能 (PF) または仮想機能 (VF) に接続してすべての拡張の情報が返されます。 PF または VF がで指定された、 **AttachedFunctionId**その構造体のメンバー。

    場合、 **AttachedFunctionId** NDIS にメンバーが設定されている\_PF\_関数\_ID、拡張のすべての情報が返されます。 これにより、VPort、PF. にアタッチされている既定値が含まれます。 場合、 **AttachedFunctionId**メンバーは、有効な VF 識別子に設定されている情報が返されますの指定した VF にアタッチされているすべての拡張。

    **注**  VPort、VF に接続できる 1 つだけの既定以外の Windows Server 2012 以降します。 ただし、(VPort の既定値を含む) 複数の拡張は、PF. に接続できます。

     

-   場合、**フラグ**メンバーが 0 に設定されている、すべての拡張が VF、PF にネットワーク アダプターの接続情報が返されます。 ここでの値、 **SwitchId**と**AttachedFunctionId**は無視されます。

NDIS ハンドル、 [OID\_NIC\_スイッチ\_ENUM\_拡張](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-vports)ミニポート ドライバーに要求します。 NDIS は、次のソースを調べることから保持されているデータの内部キャッシュから情報を返します。

-   OID メソッド要求[OID\_NIC\_スイッチ\_作成\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)します。

-   OID の要求を設定する[OID\_NIC\_スイッチ\_VPORT\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vport-parameters)します。

 

 





