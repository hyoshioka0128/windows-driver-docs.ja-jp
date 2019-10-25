---
title: 仮想関数の PCI 構成データの設定
description: 仮想関数の PCI 構成データの設定
ms.assetid: 74CAAD8B-7009-4C79-A496-93B4A3DA0B43
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fdedf519882ba93dc54ff91dc5c733f1cffa66f5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841930"
---
# <a name="setting-the-pci-configuration-data-of-a-virtual-function"></a>仮想関数の PCI 構成データの設定


PCI Express (PCIe) 仮想機能 (VF) 用のミニポートドライバーは、Hyper-v 子パーティションのゲストオペレーティングシステムで実行されます。 このため、VF ミニポートドライバーは、VF の PCI 構成領域などのハードウェアリソースに直接アクセスすることはできません。 VF の PCI 構成領域にアクセスできるのは、PCIe 物理機能 (PF) のミニポートドライバーだけです。 PF ミニポートドライバーは、Hyper-v 親パーティションの管理オペレーティングシステムで実行され、VF リソースへの特権アクセスを持ちます。

仮想化スタックなど、それまでのドライバーは、VF ミニポートドライバーが[**NdisMSetBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetbusdata)を呼び出してその PCI への書き込みを行うときに、 [\_\_vf\_\_\_SRIOV](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-write-vf-config-space)の oid セット要求を発行します。構成領域。

この OID セット要求を発行する前に、次のように、前のドライバーによって、[ **\_VF\_CONFIG\_SPACE\_PARAMETERS 構造を書き込む\_\_SRIOV**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_write_vf_config_space_parameters)のメンバーを設定する必要があります。:

-   **VFId**メンバーに、情報を書き込む VF の識別子を設定します。

-   **オフセット**メンバーを、データが書き込まれる VF の PCI 構成領域内のオフセットに設定します。

-   **Length**メンバーを、VF の PCI 構成領域に書き込むバイト数に設定します。

-   **Bufferoffset**メンバーを、指定された VF の PCI 構成領域に書き込まれるデータを格納するバッファー内のオフセット (**informationbuffer**メンバーによって参照される) に設定します。 このオフセットは、NDIS の先頭からのバイト単位で指定されます[ **\_SRIOV\_書き込み\_VF\_CONFIG\_SPACE\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_write_vf_config_space_parameters)構造体です。

Oid\_oid の OID メソッド要求を処理するときに、 [\_VF\_CONFIG\_SPACE\_書き込む](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-write-vf-config-space)場合、PF ミニポートドライバーは次のガイドラインに従う必要があります。

-   PF ミニポートドライバーは、NDIS\_SRIOV の**VFId**メンバーによって指定された vf の[ **\_\_vf\_CONFIG\_\_のパラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_write_vf_config_space_parameters)構造に書き込まれ、以前のリソースがあることを確認する必要があります。済み. PF ミニポートドライバーは、Oid\_\_の oid メソッド要求を通じて VF のリソースを割り当て[\_vf\_割り当て](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)ます。

    指定された VF のリソースが割り当てられていない場合、ドライバーは OID 要求を失敗させる必要があります。

-   PF ミニポートドライバーは、 [**NdisMSetVirtualFunctionBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetvirtualfunctionbusdata)を呼び出して、要求された PCI 構成領域に書き込みます。 ただし、PF ミニポートドライバーは、PCI 構成領域の前の読み取り操作または書き込み操作からドライバーがキャッシュした VF の PCI 構成領域データも返すことができます。

    **注**  独立系ハードウェアベンダー (IHV) が sr-iov[ドライバーパッケージ](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)の一部として仮想バスドライバー (VBD) を提供している場合、その PF ミニポートドライバーは[**NdisMSetVirtualFunctionBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetvirtualfunctionbusdata)を呼び出すことができません。 代わりに、ドライバーは、プライベート通信チャネルを介して、VBD とのインターフェイスを使用して、VBD が[*Setvirtualfunctiondata*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-set_virtual_device_data)を呼び出すように要求する必要があります。 この関数は、基になる仮想 PCI (VPCI) バスドライバーでサポートされている[GUID\_vpci\_インターフェイス\_標準](https://msdn.microsoft.com/library/windows/hardware/hh451146)インターフェイスから公開されています。

     

PF ミニポートドライバーが OID 要求を正常に完了できる場合、ドライバーは、要求された PCI 構成領域のデータを、 [**NDIS\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーによって参照されるバッファーにコピーする必要があります. ドライバーは、NDIS\_SRIOV の**Bufferoffset**メンバーによって指定されたオフセット位置にあるバッファーにデータをコピーし[ **\_\_VF\_CONFIG\_SPACE\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_space_parameters)構造体を読み取ります。

 

 





