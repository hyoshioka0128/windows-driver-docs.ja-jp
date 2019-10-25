---
title: PF ミニポート ドライバーの MiniportAddDevice ガイドライン
description: PF ミニポート ドライバーの MiniportAddDevice ガイドライン
ms.assetid: D67FDBA0-C020-4557-9199-B9FF6F91DE6B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 566ce25f785feced3acf7cd11e3c4d8a19c05b01
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844234"
---
# <a name="miniportadddevice-guidelines-for-pf-miniport-drivers"></a>PF ミニポート ドライバーの MiniportAddDevice ガイドライン


このトピックでは、PCI Express (PCIe) 物理機能 (PF) のミニポートドライバー用の[*MiniportAddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_add_device)関数を記述するためのガイドラインについて説明します。 PF は、シングルルート i/o 仮想化 (SR-IOV) をサポートするネットワークアダプターのコンポーネントです。

**注**  これらのガイドラインは、PF ミニポートドライバーにのみ適用されます。 アダプターの PCIe 仮想機能 (VF) のミニポートドライバーの初期化ガイドラインについては、「 [Vf ミニポートドライバーの初期化](initializing-a-vf-miniport-driver.md)」を参照してください。

 

プラグアンドプレイ (PnP) マネージャーは、NDIS [*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)関数を呼び出して、ネットワークアダプターの機能デバイスオブジェクト (FDO) を作成します。 PF ミニポートドライバーが[**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)という名前の[*MiniportAddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_add_device)エントリポイントを登録した場合、NDIS はドライバーの*MiniportAddDevice*関数を呼び出します。

[*MiniportAddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_add_device)が呼び出されると、PF ミニポートドライバーは、sr-iov およびネットワークインターフェイスカード (NIC) スイッチ用に追加のソフトウェアリソースを割り当てることができます。 通常、これらは、NDIS がドライバーの[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数を呼び出す前に割り当てる必要があるリソースです。

ドライバーは、 [*MiniportAddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_add_device)の呼び出しのコンテキスト内で次の操作を実行できます。

-   PF ミニポートドライバーは、 [**NdisReadConfiguration**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreadconfiguration)を呼び出して、SR-IOV と NIC スイッチの構成設定をレジストリから読み取ることができます。 これらの構成設定は、標準化された SR-IOV キーワードを使用して定義されます。 これらのキーワードの詳細については、「sr-iov の標準化された[INF キーワード](standardized-inf-keywords-for-sr-iov.md)」を参照してください。

-   これらの構成設定に基づいて、PF ミニポートドライバーによって、sr-iov ネットワークアダプター用の追加のソフトウェアリソースが割り当てられます。

ハードウェアリソースの実際の割り当てと PCI 構成領域での sr-iov の有効化は、 [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)の呼び出しのコンテキスト内でのみ実行する必要がある**ことに注意**してください  。 [*MiniportAddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_add_device)が呼び出されると、ネットワークアダプターのメモリマップト I/O (MMIO) 空間は初期化されないため、 *MiniportInitializeEx*が呼び出されるまで、ミニポートドライバーはアダプターに対して読み取りまたは書き込みを行うことができません。

 

 

 





