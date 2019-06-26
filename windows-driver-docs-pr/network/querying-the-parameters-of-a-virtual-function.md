---
title: 仮想関数のパラメーターのクエリ
description: 仮想関数のパラメーターのクエリ
ms.assetid: D834762D-9141-4F0F-B76D-5C8ABB016B64
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6313b4ebac5078c8abe526d2d0d9c60c9a5b98e0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379193"
---
# <a name="querying-the-parameters-of-a-virtual-function"></a>仮想関数のパラメーターのクエリ


上にある、ドライバーまたはユーザー モード アプリケーションを取得できます、現在のパラメーターの PCI Express (PCIe) 仮想機能 (VF) シングル ルート I/O 仮想化 (SR-IOV) をサポートするネットワーク アダプターで。 ドライバーまたはアプリケーションのオブジェクト識別子 (OID) メソッド要求を発行[OID\_NIC\_スイッチ\_VF\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vf-parameters)これらのパラメーターを取得します。

上にあるドライバーはこの OID メソッド要求を発行前に初期化する必要があります、 [ **NDIS\_NIC\_スイッチ\_VF\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)構造体。 ドライバーまたはアプリケーションを設定する必要があります、 **VFId**メンバーのパラメーターが返されるは VF の識別子。 VF 識別子は、次の方法で取得できます。

-   OID メソッド要求を発行して[OID\_NIC\_スイッチ\_ENUM\_VFS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-vfs)します。

    この OID 要求が正常に完了すると、上にあるドライバーまたはユーザー モード アプリケーションは、ネットワーク アダプターに割り当てられているすべての VFs の一覧を受け取ります。 リスト内の各要素は、 [ **NDIS\_NIC\_スイッチ\_VF\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info)構造は、指定された、 VFid**VFId**メンバー。

-   OID メソッド要求を発行して[OID\_NIC\_スイッチ\_ALLOCATE\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)します。

    上にあるドライバーがで新しく作成された VF の識別子を受け取るこの OID 要求が正常に完了している場合、 **VFId** 、返されたメンバー [ **NDIS\_NIC\_スイッチ\_VF\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)構造体。

    **注**  専用ドライバーの関連でこの方法で VF 識別子を取得できます。

     

OID メソッドの要求から正常に戻った後、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体ポインターが含まれています、 [ **NDIS\_NIC\_スイッチ\_VF\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)構造体。 この構造体には、指定した VF の構成パラメーターが含まれています。

NDIS ハンドル、 [OID\_NIC\_スイッチ\_VF\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vf-parameters)ミニポート ドライバーに要求します。 NDIS は、次のソースを調べることから保持されているデータの内部キャッシュから情報を返します。

-   OID メソッド要求[OID\_NIC\_スイッチ\_ALLOCATE\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)します。

-   OID の要求を設定する[OID\_NIC\_スイッチ\_VF\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vf-parameters)します。

 

 





