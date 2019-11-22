---
title: 仮想関数の PCI ベンダーとデバイス Id を照会する
description: 仮想関数の PCI ベンダーおよびデバイス ID のクエリ
ms.assetid: A2FB0A35-A89B-4028-92BA-E75739B080FD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f4430d9b78e94a6b495d037c840f6fb692c35b4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844867"
---
# <a name="querying-the-pci-vendor-and-device-identifiers-for-a-virtual-function"></a>仮想関数の PCI ベンダーおよびデバイス ID のクエリ

**メモ**この方法は、Hyper-v の親パーティションの管理オペレーティングシステムで実行されるドライバーによってのみ使用できます。

PCI Express (PCIe) ベンダー識別子 (*VendorID*) とデバイス Id (*DeviceID*) に対してクエリを実行するために、その後のドライバーが[oid\_SRIOV\_VF\_ベンダー\_デバイス\_ID](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-vf-vendor-device-id)のオブジェクト識別子 (oid) メソッド要求を発行します。 このデータは、物理ネットワークアダプターの PCIe 仮想機能 (VF) 用の PCIe 構成領域から読み取られます。

この OID メソッドの要求は、ネットワークアダプターの PCI Express (PCIe) 物理機能 (PF) のミニポートドライバーに発行されます。 この OID メソッド要求は、シングルルート i/o 仮想化 (SR-IOV) インターフェイスをサポートする PF ミニポートドライバーに必要です。

Hyper-v 子パーティションで実行されているゲストオペレーティングシステムでは、デバイスの列挙に VendorID (汎用プラグアンドプレイ (PnP) Id の VF のと DeviceID を使用します。 Windows Server 2012 以降、PF ミニポートドライバーは、子パーティションで公開されている VF ネットワークアダプターに対して次の一連の識別子を提供できます。

-   物理ネットワークアダプターの VendorID と DeviceID。 これにより、互換性のあるドライバーを、hyper-v 子パーティションで実行されているゲストオペレーティングシステムと、Hyper-v の親パーティションで実行されている管理オペレーティングシステムに読み込むことができます。

-   物理ネットワークアダプターの識別子とは異なる VendorID と DeviceID。 これにより、ドライバーをゲストオペレーティングシステムに読み込んで、その用途に適したものにすることができます。 たとえば、PF ミニポートドライバーは、VF ネットワークアダプターの VendorID と DeviceID を返して、電源管理やプロトコルタスクのオフロードなどの特定の機能セットを無効にするドライバーが読み込まれるようにすることができます。

この OID メソッド要求を発行する前に、前のドライバーは、 [**NDIS\_SRIOV\_VF\_ベンダー\_デバイス\_ID\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_vf_vendor_device_id_info)構造体を初期化する必要があります。 ドライバーは、 **VFId**メンバーを、情報の読み取り元となる VF の識別子に設定する必要があります。

この OID 要求を処理するとき、PF ミニポートドライバーは、指定された VF に以前に割り当てられたリソースがあることを確認する必要があります。 PF ミニポートドライバーは、oid の OID メソッド要求中に、 [\_NIC\_スイッチによって\_vf\_割り当てら](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)れるため、vf のリソースを割り当てます。 指定された VF のリソースが割り当てられていない場合、ドライバーは OID 要求を失敗させる必要があります。

 

 





