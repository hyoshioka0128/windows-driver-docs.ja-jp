---
title: PF ミニポート ドライバーの DriverEntry ガイドライン
description: PF ミニポート ドライバーの DriverEntry ガイドライン
ms.assetid: 6F885379-41EC-411E-8909-4DF48042849A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69c2cc2ff57eba7f7f92599e2c405d88b43f88fd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386551"
---
# <a name="driverentry-guidelines-for-pf-miniport-drivers"></a>PF ミニポート ドライバーの DriverEntry ガイドライン


このトピックでは、書き込みのためのガイドラインを説明します、 [ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/network/initializing-a-miniport-driver)ミニポート ドライバーの PCI Express (PCIe) 物理機能 (PF) の関数。 PF は、シングル ルート I/O 仮想化 (SR-IOV) をサポートするネットワーク アダプターのコンポーネントです。

**注**  次のガイドラインは、PF ミニポート ドライバーにのみ適用されます。 PCIe 仮想機能 (VF) アダプターのミニポート ドライバーの初期化ガイドラインについては、次を参照してください。 [VF のミニポート ドライバーの初期化](initializing-a-vf-miniport-driver.md)します。

 

SR-IOV ネットワーク アダプターには、アダプターの物理ポートと内部仮想ポート (拡張) 経由でネットワーク トラフィックを転送するハードウェア ブリッジを実装する必要があります。 このブリッジと呼ばれる、 *NIC スイッチ*します。 詳細については、次を参照してください。 [NIC スイッチ](nic-switches.md)します。

PF のミニポート ドライバーでは、SR-IOV ネットワーク アダプターの静的 NIC スイッチの作成をサポートする場合は、デバイス スタック内のネットワーク アダプターの機能のデバイス オブジェクト (FDO) が作成されるときに、スイッチのリソースを割り当てる必要があります。 この場合、ドライバーが NDIS 呼び出される前にこれらのリソースを割り当てる必要があります[ *MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)します。 これを行うには、アダプターの FDO を追加またはデバイス スタックから削除されたときに、プロセスに参加するように、ドライバーは省略可能なプラグ アンド プレイ (PnP) ハンドラーを登録する必要があります。

ミニポート ドライバーを提供する必要があります、 [ *MiniportSetOptions* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)これら PnP ハンドラー関数を登録する関数。 これを行うには、ドライバーはへの呼び出しのコンテキストからこれらの手順を次の[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/network/initializing-a-miniport-driver)関数。

1.  ミニポート ドライバーを初期化します、 [ **NDIS\_ミニポート\_ドライバー\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_driver_characteristics)のエントリ ポイントを含む構造体、 *MiniportXxx*関数。 具体的には、ドライバーの設定、 **SetOptionsHandler**のドライバーのエントリ ポイントをメンバー [ *MiniportSetOptions* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)関数。

2.  ミニポート ドライバーの呼び出し、 [ **NdisMRegisterMiniportDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterminiportdriver)そのエントリ ポイントを登録する関数。 NDIS ドライバーの呼び出し、この呼び出しのコンテキストから[ *MiniportSetOptions* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)関数

3.  NDIS を呼び出すと[ *MiniportSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)、ミニポート ドライバーの呼び出し、 [ **NdisSetOptionalHandlers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissetoptionalhandlers)関数を指定します。[ **NDIS\_ミニポート\_PNP\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_pnp_characteristics)構造体。 この構造体のエントリ ポイントを定義する、 [ *MiniportAddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_add_device)、 [ *MiniportRemoveDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_remove_device)、 [ *MiniportStartDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_pnp_irp)、および[ *MiniportFilterResourceRequirements* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_pnp_irp)関数。 NDIS は、PCI バス ドライバーによって発行された PnP I/O 要求パケット (Irp) を処理するときに、これらのハンドラー関数を呼び出します。

    NDIS ドライバーを呼び出す前に、PF ミニポート ドライバーする必要があります NIC スイッチに追加のソフトウェアのリソースを割り当てるかどうか[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数の場合、ドライバーを登録する必要があります、 [*MiniportAddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_add_device)関数。 NDIS を呼び出すと、 *MiniportAddDevice* PF ミニポート ドライバーが呼び出すことができます関数、 [**エミュレーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisreadconfiguration) NIC スイッチ構成キーワードの設定を読み取るレジストリから。 これらのキーワードの詳細については、次を参照してください。 [SR-IOV の標準化された INF キーワード](standardized-inf-keywords-for-sr-iov.md)します。

    に関するガイドラインの詳細については、 [ *MiniportAddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_add_device)関数を参照してください[ *MiniportAddDevice* PF ミニポート ドライバーに関するガイドライン](miniportadddevice-guidelines-for-pf-miniport-drivers.md).

NIC のスイッチを作成する方法の詳細については、次を参照してください。 [NIC スイッチの作成](creating-a-nic-switch.md)です。

 

 





