---
title: 仮想関数の PCI 構成領域のクエリ
description: 仮想関数の PCI 構成領域のクエリ
ms.assetid: FFE7C946-4406-46A5-A9A7-CD0E2756C98E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a2d042950837655d8fdd253ee1054cca137ddc41
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844872"
---
# <a name="querying-the-pci-configuration-space-for-a-virtual-function"></a>仮想関数の PCI 構成領域のクエリ

**メモ**この方法は、Hyper-v の親パーティションの管理オペレーティングシステムで実行されるドライバーによってのみ使用できます。

PCI Express (PCIe) 仮想機能 (VF) 用のミニポートドライバーは、Hyper-v 子パーティションのゲストオペレーティングシステムで実行されます。 このため、VF ミニポートドライバーは、VF の PCIe 構成領域などのハードウェアリソースに直接アクセスすることはできません。 VF の PCIe 構成領域にアクセスできるのは、PCIe 物理機能 (PF) のミニポートドライバーだけです。 PF ミニポートドライバーは、Hyper-v 親パーティションの管理オペレーティングシステムで実行され、VF リソースへの特権アクセスを持ちます。

管理オペレーティングシステムで実行されているその後のドライバーが、オブジェクト識別子 (OID) のメソッド要求を[oid\_SRIOV\_読み取り\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-read-vf-config-space)の構成領域からデータを読み取るために、\_構成\_ネットワークアダプター上で指定された VF。

たとえば、管理オペレーティングシステムで実行されている仮想化スタックは、vf の\_SRIOV の oid メソッド要求を発行します。これは、vf ミニポートドライバーが[**NdisMGetBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismgetbusdata)を呼び出して vf\_の PCIe 構成領域から読み取るときに、 [\_vf\_CONFIG\_SPACE を読み取る](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-read-vf-config-space)ことができます。

この OID メソッドの要求を発行する前に、次のように、前のドライバーで、[ **\_VF\_CONFIG\_SPACE\_PARAMETERS 構造体の\_\_SRIOV**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_space_parameters)のメンバーを設定する必要があります。:

-   **VFId**メンバーには、情報の読み取り元となる VF の識別子を設定する必要があります。

-   **オフセット**メンバーは、データが読み込まれる VF の PCIe 構成領域内のオフセットに設定されている必要があります。

-   **長さ**のメンバーは、VF の PCIe 構成領域から読み取るバイト数に設定する必要があります。

-   **Bufferoffset**メンバーは、指定された VF の PCI 構成領域から読み取られるデータを格納するバッファー内のオフセット ( **informationbuffer**メンバーによって参照される) に設定する必要があります。 このオフセットは、NDIS\_SRIOV の先頭からのバイト単位で指定されています。 [ **\_読み取り\_VF\_CONFIG\_の\_のパラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_space_parameters)構造体です。

Oid\_oid の OID メソッド要求を処理するときに、 [\_VF\_CONFIG\_SPACE\_読み取る](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-read-vf-config-space)ために、PF ミニポートドライバーは次のガイドラインに従う必要があります。

-   ミニポートドライバーは、NDIS\_SRIOV の**VFId**メンバーによって指定された vf の[ **\_\_vf\_CONFIG\_\_のパラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_space_parameters)構造に含まれていた、以前のリソースがあることを確認する必要があります。済み. ミニポートドライバーは、Oid\_の oid メソッド要求を通じて VF のリソースを割り当てます。これにより[\_vf\_割り当て、NIC\_切り替わり](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)ます。 指定された VF のリソースが割り当てられていない場合、ドライバーは OID 要求を失敗させる必要があります。

-   ミニポートドライバーは、要求された PCIe 構成領域のデータを返すために十分な大きさ**のバッファー (** [**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造) を確認する必要があります。 これが true でない場合、ドライバーは OID 要求を失敗させる必要があります。
-   通常、ミニポートドライバーは[**NdisMGetVirtualFunctionBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismgetvirtualfunctionbusdata)を呼び出して、要求された PCIe 構成領域に対してクエリを実行します。 ただし、ミニポートドライバーは、PCIe 構成領域の以前の読み取り操作または書き込み操作からドライバーがキャッシュした VF の PCIe 構成領域データも返すことができます。

    **注**  、独立系ハードウェアベンダー (IHV) が sr-iov[ドライバーパッケージ](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)の一部として仮想バスドライバー (VBD) を提供している場合、そのミニポートドライバーは[**NdisMGetVirtualFunctionBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismgetvirtualfunctionbusdata)を呼び出すことができません。 代わりに、ドライバーは、プライベート通信チャネルを介して、VBD とのインターフェイスを使用して、.VBD に[*Readvfconfigblock*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh439637(v=vs.85))を呼び出すように要求する必要があります。 この関数は、基になる仮想 PCI (VPCI) バスドライバーでサポートされている[GUID\_vpci\_インターフェイス\_標準](https://msdn.microsoft.com/library/windows/hardware/hh451146)インターフェイスから公開されています。

     

この OID メソッド要求から正常に戻った後、 [**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、呼び出し元が割り当てたバッファーへのポインターが含まれます。 このバッファーは、次のものが含まれるように書式設定されます。

-   NDIS\_SRIOV は、VF の PCIe 構成領域の読み取り操作のためのパラメーターを格納する[ **\_vf\_CONFIG\_SPACE\_parameters 構造\_読み取り**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_space_parameters)ます。

-   PCIe 構成領域から読み取るデータ用の追加のバッファー領域。 ドライバーは、NDIS\_SRIOV の**Bufferoffset**メンバーによって指定されたオフセット位置にあるバッファーにデータをコピーし[ **\_\_VF\_CONFIG\_SPACE\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_space_parameters)構造体を読み取ります。

 

 





