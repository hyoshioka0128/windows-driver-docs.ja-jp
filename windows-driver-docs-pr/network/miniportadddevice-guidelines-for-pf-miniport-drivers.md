---
title: PF ミニポート ドライバーの MiniportAddDevice ガイドライン
description: PF ミニポート ドライバーの MiniportAddDevice ガイドライン
ms.assetid: D67FDBA0-C020-4557-9199-B9FF6F91DE6B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21619f7deaa5c5bad25a523ce92fe49779292428
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380882"
---
# <a name="miniportadddevice-guidelines-for-pf-miniport-drivers"></a>PF ミニポート ドライバーの MiniportAddDevice ガイドライン


このトピックでは、書き込みのためのガイドラインを説明します、 [ *MiniportAddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_add_device)ミニポート ドライバーの PCI Express (PCIe) 物理機能 (PF) の関数。 PF は、シングル ルート I/O 仮想化 (SR-IOV) をサポートするネットワーク アダプターのコンポーネントです。

**注**  次のガイドラインは、PF ミニポート ドライバーにのみ適用されます。 PCIe 仮想機能 (VF) アダプターのミニポート ドライバーの初期化ガイドラインについては、次を参照してください。 [VF のミニポート ドライバーの初期化](initializing-a-vf-miniport-driver.md)します。

 

プラグ アンド プレイ (PnP) マネージャーには、NDIS [ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)ネットワーク アダプターの機能のデバイス オブジェクト (FDO) を作成する関数。 PF のミニポート ドライバーに登録されている場合、 [ *MiniportAddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_add_device)エントリ ポイントが呼び出されたときに[ **NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterminiportdriver)、NDISドライバーの呼び出す*MiniportAddDevice*関数。

ときに[ *MiniportAddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_add_device)が呼び出され、PF ミニポート ドライバーは、SR-IOV とネットワーク インターフェイス カード (NIC) スイッチの追加のソフトウェアのリソースを割り当てることができます。 通常、これらは、NDIS ドライバーを呼び出す前に割り当てる必要があるリソース[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数。

ドライバーがへの呼び出しのコンテキスト内で、次の操作を行います[ *MiniportAddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_add_device):

-   PF のミニポート ドライバーを呼び出すことができます[**エミュレーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisreadconfiguration)を読み取る、SR-IOV と NIC は、レジストリから構成設定を切り替えます。 これらの構成設定は、標準化された SR-IOV キーワードによって定義されます。 これらのキーワードの詳細については、次を参照してください。 [SR-IOV の標準化された INF キーワード](standardized-inf-keywords-for-sr-iov.md)します。

-   これらの構成設定に基づき、PF ミニポート ドライバーは、SR-IOV ネットワーク アダプターの追加のソフトウェアのリソースを割り当てます。

**注**  への呼び出しのコンテキスト内でハードウェア リソースの実際の割り当てと PCI 構成領域で sr-iov を有効化を実行する必要がありますのみ[ *MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize). ネットワーク アダプターのメモリ マップ I/O (MMIO) の領域が初期化されていない場合に[ *MiniportAddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_add_device)と呼ばれる場合は、ミニポート ドライバーの読み取りまたは書き込みまでアダプターをする必要がありますいない*MiniportInitializeEx*が呼び出されます。

 

 

 





