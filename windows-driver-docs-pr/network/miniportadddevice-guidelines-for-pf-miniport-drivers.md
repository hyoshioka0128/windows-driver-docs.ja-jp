---
title: PF ミニポート ドライバー MiniportAddDevice ガイドライン
description: PF ミニポート ドライバー MiniportAddDevice ガイドライン
ms.assetid: D67FDBA0-C020-4557-9199-B9FF6F91DE6B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76d3f86315c42456580a13f8bc893b8fd0e03c12
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538552"
---
# <a name="miniportadddevice-guidelines-for-pf-miniport-drivers"></a>PF ミニポート ドライバー MiniportAddDevice ガイドライン


このトピックでは、書き込みのためのガイドラインを説明します、 [ *MiniportAddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff559332)ミニポート ドライバーの PCI Express (PCIe) 物理機能 (PF) の関数。 PF は、シングル ルート I/O 仮想化 (SR-IOV) をサポートするネットワーク アダプターのコンポーネントです。

**注**  次のガイドラインは、PF ミニポート ドライバーにのみ適用されます。 PCIe 仮想機能 (VF) アダプターのミニポート ドライバーの初期化ガイドラインについては、次を参照してください。 [VF のミニポート ドライバーの初期化](initializing-a-vf-miniport-driver.md)します。

 

プラグ アンド プレイ (PnP) マネージャーには、NDIS [ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)ネットワーク アダプターの機能のデバイス オブジェクト (FDO) を作成する関数。 PF のミニポート ドライバーに登録されている場合、 [ *MiniportAddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff559332)エントリ ポイントが呼び出されたときに[ **NdisMRegisterMiniportDriver**](https://msdn.microsoft.com/library/windows/hardware/ff563654)、NDISドライバーの呼び出す*MiniportAddDevice*関数。

ときに[ *MiniportAddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff559332)が呼び出され、PF ミニポート ドライバーは、SR-IOV とネットワーク インターフェイス カード (NIC) スイッチの追加のソフトウェアのリソースを割り当てることができます。 通常、これらは、NDIS ドライバーを呼び出す前に割り当てる必要があるリソース[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数。

ドライバーがへの呼び出しのコンテキスト内で、次の操作を行います[ *MiniportAddDevice*](https://msdn.microsoft.com/library/windows/hardware/ff559332):

-   PF のミニポート ドライバーを呼び出すことができます[**エミュレーター** ](https://msdn.microsoft.com/library/windows/hardware/ff564511)を読み取る、SR-IOV と NIC は、レジストリから構成設定を切り替えます。 これらの構成設定は、標準化された SR-IOV キーワードによって定義されます。 これらのキーワードの詳細については、次を参照してください。 [SR-IOV の標準化された INF キーワード](standardized-inf-keywords-for-sr-iov.md)します。

-   これらの構成設定に基づき、PF ミニポート ドライバーは、SR-IOV ネットワーク アダプターの追加のソフトウェアのリソースを割り当てます。

**注**  への呼び出しのコンテキスト内でハードウェア リソースの実際の割り当てと PCI 構成領域で sr-iov を有効化を実行する必要がありますのみ[ *MiniportInitializeEx*](https://msdn.microsoft.com/library/windows/hardware/ff559389). ネットワーク アダプターのメモリ マップ I/O (MMIO) の領域が初期化されていない場合に[ *MiniportAddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff559332)と呼ばれる場合は、ミニポート ドライバーの読み取りまたは書き込みまでアダプターをする必要がありますいない*MiniportInitializeEx*が呼び出されます。

 

 

 





