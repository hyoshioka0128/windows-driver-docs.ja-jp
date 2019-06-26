---
title: 仮想関数の PCI 構成領域のクエリ
description: 仮想関数の PCI 構成領域のクエリ
ms.assetid: FFE7C946-4406-46A5-A9A7-CD0E2756C98E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4de4edfcbe26efca003a323ee697af762ab442ae
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377050"
---
# <a name="querying-the-pci-configuration-space-for-a-virtual-function"></a>仮想関数の PCI 構成領域のクエリ

**注**このメソッドは、HYPER-V 親パーティションの管理オペレーティング システムで実行されているドライバーの関連でのみ使用できます。

ミニポート ドライバーを PCI Express (PCIe) 仮想機能 (VF) は、HYPER-V 子パーティションのゲスト オペレーティング システムで実行されます。 このため、VF のミニポート ドライバーは VF の PCIe 構成領域などのハードウェア リソースを直接アクセスすることはできません。 ミニポート ドライバー PCIe 物理機能 (PF) にのみを VF の PCIe 構成領域にアクセスできます。 PF のミニポート ドライバーでは、HYPER-V 親パーティションの管理オペレーティング システムで実行され、VF リソースへのアクセスには特権します。

管理オペレーティング システムで実行されている上位のドライバーの問題のオブジェクト識別子 (OID) メソッド要求[OID\_SRIOV\_読み取り\_VF\_CONFIG\_領域](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-read-vf-config-space)ネットワーク アダプターで指定された VF の PCIe 構成領域からデータを読み取る。

管理オペレーティング システムで実行されている仮想化スタックがの OID メソッド要求を発行するなど、 [OID\_SRIOV\_読み取り\_VF\_CONFIG\_領域](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-read-vf-config-space)VF のミニポート ドライバーを呼び出すと[ **NdisMGetBusData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismgetbusdata) PCIe の VF 構成領域からの読み取り。

この OID メソッド要求を発行する前に、上にあるドライバーがのメンバーを設定する必要があります、[**NDIS\_SRIOV\_読み取り\_VF\_CONFIG\_領域\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_space_parameters)次のように構造体。

-   **VFId**メンバーは、元の情報が読み取られる VF の識別子を設定する必要があります。

-   **オフセット**メンバーは、データが読み取られる VF の PCIe 構成領域内のオフセットを設定する必要があります。

-   **長さ**メンバーは、VF の PCIe 構成領域から読み取るバイト数に設定する必要があります。

-   **BufferOffset**メンバーは、バッファー内のオフセットを設定する必要があります (によって参照される、 **InformationBuffer**メンバー) を指定した VF の PCI 構成領域から読み取られるデータを含む. このオフセットがの先頭からバイト単位で指定された、 [ **NDIS\_SRIOV\_読み取り\_VF\_CONFIG\_領域\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_space_parameters)構造体。

OID メソッド要求を処理するときに[OID\_SRIOV\_読み取り\_VF\_CONFIG\_領域](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-read-vf-config-space)、PF ミニポート ドライバーが次のガイドラインに従う必要があります。

-   ミニポート ドライバーは、VF がで指定されたを確認する必要があります、 **VFId**のメンバー、 [ **NDIS\_SRIOV\_読み取り\_VF\_CONFIG\_領域\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_space_parameters)構造体を以前に割り当てられているリソースします。 ミニポート ドライバーは VF の OID メソッドの要求からのリソースの割り当て[OID\_NIC\_スイッチ\_ALLOCATE\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)します。 指定した VF 用のリソースが割り当てられていない場合、ドライバーは OID 要求に失敗する必要があります。

-   ミニポート ドライバーを確認する必要がありますバッファー (によって参照される、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体) は、要求された PCIe 構成領域のデータを返すのに十分な大きさです。 True でない場合、ドライバーは、OID 要求を失敗する必要があります。
-   通常、ミニポート ドライバーを呼び出します[ **NdisMGetVirtualFunctionBusData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismgetvirtualfunctionbusdata)要求 PCIe 構成領域をクエリします。 ただし、ミニポート ドライバーには VF ドライバーが前のキャッシュの PCIe 構成領域のデータの読み取りや書き込み操作、PCIe 構成領域の取得もできます。

    **注**  独立系ハードウェア ベンダー (IHV) が SR-IOV 対応の一部としてバーチャル バス ドライバー (VBD) を提供する場合[ドライバー パッケージ](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)、ミニポート ドライバーを呼び出してはならない[ **NdisMGetVirtualFunctionBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismgetvirtualfunctionbusdata)します。 代わりに、ドライバーをプライベートな通信チャネルを介して VBD とのインターフェイスし、VBD を呼び出すことを要求する必要があります[ *ReadVfConfigBlock*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh439637(v=vs.85))します。 この関数がから公開されている、 [GUID\_VPCI\_インターフェイス\_標準](https://msdn.microsoft.com/library/windows/hardware/hh451146)基になる仮想 PCI (VPCI) バス ドライバーによってサポートされているインターフェイス。

     

この OID メソッド要求から正常に戻った後、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体呼び出し元が割り当てたバッファーへのポインターが含まれています。 このバッファーは、以下を格納する形式です。

-   [ **NDIS\_SRIOV\_読み取り\_VF\_CONFIG\_領域\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_space_parameters)構造が含まれていますが、VF の PCIe 構成領域の読み取り操作のパラメーターです。

-   PCIe 構成領域から読み取られるデータの追加バッファー領域。 ドライバーで指定されたオフセットからバッファーへのデータのコピー、**BufferOffset**のメンバー、 [ **NDIS\_SRIOV\_読み取り\_VF\_構成\_領域\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_space_parameters)構造体。

 

 





