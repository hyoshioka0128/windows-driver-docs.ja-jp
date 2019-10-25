---
title: PF ミニポート ドライバーの DriverEntry ガイドライン
description: PF ミニポート ドライバーの DriverEntry ガイドライン
ms.assetid: 6F885379-41EC-411E-8909-4DF48042849A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: accbf48f956754a0e38ef05d4baec396c73186e8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838132"
---
# <a name="driverentry-guidelines-for-pf-miniport-drivers"></a>PF ミニポート ドライバーの DriverEntry ガイドライン


このトピックでは、PCI Express (PCIe) 物理機能 (PF) のミニポートドライバー用の[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/network/initializing-a-miniport-driver)機能を記述するためのガイドラインについて説明します。 PF は、シングルルート i/o 仮想化 (SR-IOV) をサポートするネットワークアダプターのコンポーネントです。

**注**  これらのガイドラインは、PF ミニポートドライバーにのみ適用されます。 アダプターの PCIe 仮想機能 (VF) のミニポートドライバーの初期化ガイドラインについては、「 [Vf ミニポートドライバーの初期化](initializing-a-vf-miniport-driver.md)」を参照してください。

 

SR-IOV ネットワークアダプターは、アダプターの物理ポートと内部仮想ポート (VPorts) を介してネットワークトラフィックを転送するハードウェアブリッジを実装する必要があります。 このブリッジは、 *NIC スイッチ*と呼ばれています。 詳細については、「 [NIC スイッチ](nic-switches.md)」を参照してください。

PF ミニポートドライバーが sr-iov ネットワークアダプターでの NIC スイッチの静的作成をサポートしている場合、デバイススタックのネットワークアダプターに対して機能デバイスオブジェクト (FDO) が作成されるときに、スイッチリソースの割り当てが必要になることがあります。 この場合、NDIS が[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)を呼び出す前に、ドライバーがこれらのリソースを割り当てる必要があります。 これを行うには、ドライバーはオプションのプラグアンドプレイ (PnP) ハンドラーを登録して、アダプターの FDO がデバイススタックから追加または削除されたときにプロセスに参加できるようにする必要があります。

ミニポートドライバーは、これらの PnP ハンドラー関数を登録するための[*MiniportSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)関数を提供する必要があります。 これを行うには、ドライバーは[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/network/initializing-a-miniport-driver)関数の呼び出しのコンテキストから次の手順を実行します。

1.  ミニポートドライバーは、 *Miniportxxx*関数のエントリポイントを使用して、 [**NDIS\_ミニポート\_ドライバー\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics)の構造を初期化します。 特に、ドライバーは**SetOptionsHandler**メンバーをドライバーの[*MiniportSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)関数のエントリポイントに設定します。

2.  ミニポートドライバーは、エントリポイントを登録するために[**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)関数を呼び出します。 この呼び出しのコンテキストから、NDIS はドライバーの[*MiniportSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)関数を呼び出します。

3.  NDIS が[*MiniportSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)を呼び出すと、ミニポートドライバーは[**NdisSetOptionalHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers)関数を呼び出し、 [**NDIS\_ミニポート\_PNP\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_pnp_characteristics)の構造を指定します。 この構造体は、 [*MiniportAddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_add_device)、 [*miniportremovedevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_remove_device)、 [*miniportremovedevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pnp_irp)、および[*MiniportFilterResourceRequirements*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pnp_irp)関数のエントリポイントを定義します。 NDIS は、PCI バスドライバーによって発行された PnP i/o 要求パケット (Irp) を処理するときに、これらのハンドラー関数を呼び出します。

    NDIS がドライバーの[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数を呼び出す前に、PF ミニポートドライバーが NIC スイッチ用に追加のソフトウェアリソースを割り当てる必要がある場合、ドライバーは[*MiniportAddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_add_device)関数を登録する必要があります。 NDIS が*MiniportAddDevice*関数を呼び出すと、PF ミニポートドライバーは[**NdisReadConfiguration**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreadconfiguration)を呼び出して、レジストリから NIC スイッチ構成キーワードの設定を読み取ることができます。 これらのキーワードの詳細については、「sr-iov の標準化された[INF キーワード](standardized-inf-keywords-for-sr-iov.md)」を参照してください。

    [*MiniportAddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_add_device)関数のガイドラインの詳細については、「 [ *MiniportAddDevice*の PF ミニポートドライバーのガイドライン](miniportadddevice-guidelines-for-pf-miniport-drivers.md)」を参照してください。

NIC スイッチの作成方法の詳細については、「 [Nic スイッチの作成](creating-a-nic-switch.md)」を参照してください。

 

 





