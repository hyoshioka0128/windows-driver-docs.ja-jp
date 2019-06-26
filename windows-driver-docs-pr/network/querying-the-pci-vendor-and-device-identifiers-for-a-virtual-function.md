---
title: 仮想関数の PCI ベンダーとデバイス Id のクエリを実行します。
description: 仮想関数の PCI ベンダーおよびデバイス ID のクエリ
ms.assetid: A2FB0A35-A89B-4028-92BA-E75739B080FD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4cd48b27dc3abf8e377c50910adc65473fafe9ca
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377040"
---
# <a name="querying-the-pci-vendor-and-device-identifiers-for-a-virtual-function"></a>仮想関数の PCI ベンダーおよびデバイス ID のクエリ

**注**このメソッドは、HYPER-V 親パーティションの管理オペレーティング システムで実行されているドライバーの関連でのみ使用できます。

上位のドライバーの問題のオブジェクト識別子 (OID) メソッド要求[OID\_SRIOV\_VF\_ベンダー\_デバイス\_ID](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-vf-vendor-device-id) PCI Express (PCIe) ベンダーを照会するには識別子 (*VendorID*) とデバイスの識別子 (*DeviceID*)。 物理ネットワーク アダプターの PCIe 仮想機能 (VF) の PCIe 構成領域からこのデータが読み取られます。

上にあるドライバーは、、PCI Express (PCIe) 物理機能 (PF) ネットワーク アダプターのミニポート ドライバーをこの OID メソッド要求を発行します。 この OID メソッド要求は、PF ミニポート ドライバー シングル ルート I/O 仮想化 (SR-IOV) インターフェイスをサポートする必要があります。

HYPER-V 子パーティションで実行され、ゲスト オペレーティング システムでは、デバイスの列挙のジェネリックのプラグ アンド プレイ (PnP) Id を VendorID および VF の DeviceID を使用します。 Windows Server 2012 以降では、PF ミニポート ドライバーは、子パーティションで公開されている VF のネットワーク アダプターに対して次の識別子のセットを指定できます。

-   VendorID と物理ネットワーク アダプターの DeviceID です。 これにより、互換性のあるドライバー HYPER-V 子パーティションで実行され、ゲスト オペレーティング システムと HYPER-V 親パーティションで実行される管理オペレーティング システムに読み込むことができます。

-   VendorID と DeviceID を物理ネットワーク アダプターの識別子とは異なります。 これにより、ドライバーの使用に適しているゲスト オペレーティング システムに読み込むことができます。 たとえば、PF ミニポート ドライバー返す可能性があります VendorID および DeviceID VF のネットワーク アダプターのドライバーが読み込まれるように、特定の機能セットを無効にする電源管理またはプロトコルのタスクのオフロードなど。

この OID メソッド要求を発行して、前に、上にあるドライバーを初期化する必要があります、 [ **NDIS\_SRIOV\_VF\_ベンダー\_デバイス\_ID\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_vf_vendor_device_id_info)構造体。 ドライバーを設定する必要があります、 **VFId**メンバーを元の情報が読み取られる VF の識別子。

この OID 要求を処理する場合、PF ミニポート ドライバーする必要があります指定 VF に以前割り当てられたリソースを確認します。 PF のミニポート ドライバーを VF 用のリソースの割り当ての OID メソッド要求中に[OID\_NIC\_スイッチ\_ALLOCATE\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)します。 指定した VF 用のリソースが割り当てられていない場合、ドライバーは OID 要求に失敗する必要があります。

 

 





