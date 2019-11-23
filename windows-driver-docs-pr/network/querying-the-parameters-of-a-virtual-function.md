---
title: 仮想関数のパラメーターのクエリ
description: 仮想関数のパラメーターのクエリ
ms.assetid: D834762D-9141-4F0F-B76D-5C8ABB016B64
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d14d13b42510146498045deb9ac21eb1ef71978e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844876"
---
# <a name="querying-the-parameters-of-a-virtual-function"></a>仮想関数のパラメーターのクエリ


1つ前のドライバーまたはユーザーモードアプリケーションは、シングルルート i/o 仮想化 (SR-IOV) をサポートするネットワークアダプター上の PCI Express (PCIe) 仮想関数 (VF) の現在のパラメーターを取得できます。 ドライバーまたはアプリケーションは、Oid\_NIC のオブジェクト識別子 (OID) メソッド要求を発行して、これらのパラメーターを取得するために[VF\_パラメーター\_\_切り替え](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vf-parameters)ます。

それまでのドライバーがこの OID メソッド要求を発行する前に、 [**NDIS\_NIC\_スイッチ\_VF\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)構造体を初期化する必要があります。 ドライバーまたはアプリケーションは、パラメーターが返される VF の識別子に**VFId**メンバーを設定する必要があります。 VF 識別子は、次の方法で取得できます。

-   Oid\_oid の OID メソッド要求を発行すると、 [\_列挙型\_VFS\_切り替わり](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-vfs)ます。

    この OID 要求が正常に完了した場合、それ以降のドライバーまたはユーザーモードアプリケーションは、ネットワークアダプターに割り当てられているすべての VFs の一覧を受け取ります。 リスト内の各要素は、 **VFId**メンバーによって指定された vf 識別子を使用して、 [ **\_の vf\_INFO 構造体\_スイッチの NDIS\_NIC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info)です。

-   Oid\_oid の OID メソッド要求を発行することによって、 [\_VF\_割り当て\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)ます。

    この OID 要求が正常に完了すると、新しく作成された VF の識別子が、返された[**NDIS\_NIC\_スイッチ\_VF\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)構造体の**VFId**メンバーに渡されます。

    **注**  は、この方法で VF 識別子を取得できるのは、それまでのドライバーのみです。

     

OID メソッド要求から正常に戻った後、 [**ndis\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、 [**ndis\_NIC\_スイッチ\_VF\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)構造体へのポインターが含まれています。 この構造体には、指定された VF の構成パラメーターが含まれています。

NDIS は、ミニポートドライバーの\_VF\_PARAMETERS 要求を使用して、 [OID\_NIC\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vf-parameters)を処理します。 NDIS は、次のソースを検査して、管理するデータの内部キャッシュから情報を返します。

-   Oid\_\_スイッチの OID メソッド要求では[\_VF\_割り当てる](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)ことができます。

-   Oid\_\_の oid 設定要求は、 [VF\_パラメーター\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vf-parameters)ます。

 

 





