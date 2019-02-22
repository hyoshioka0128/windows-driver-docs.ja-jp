---
title: PF のミニポート ドライバーの初期化シーケンス
description: PF のミニポート ドライバーの初期化シーケンス
ms.assetid: A8891D72-314D-4648-ABCA-E917C3091FF6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31b29dd4740a80835f7b45c4ae8abdaab29259e5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557345"
---
# <a name="initialization-sequence-for-pf-miniport-drivers"></a>PF のミニポート ドライバーの初期化シーケンス


ここでは、、PCI Express (PCIe) 物理機能 (PF) の要件とミニポート ドライバーの初期化シーケンスのガイドラインを示します。 PF は、シングル ルート I/O 仮想化 (SR-IOV) をサポートするネットワーク アダプターのコンポーネントです。

ここでは、次のトピックについて説明します。

[PF ミニポート ドライバー DriverEntry ガイドライン](driverentry-guidelines-for-pf-miniport-drivers.md)

[*MiniportAddDevice* PF ミニポート ドライバーに関するガイドライン](miniportadddevice-guidelines-for-pf-miniport-drivers.md)

[*MiniportInitializeEx* PF ミニポート ドライバーに関するガイドライン](miniportinitializeex-guidelines-for-pf-miniport-drivers.md)

**注**  の PCIe 仮想機能 (VF)、SR-IOV ネットワーク アダプターのミニポート ドライバーの初期化方法の詳細については、次を参照してください。 [VF のミニポート ドライバーの初期化](initializing-a-vf-miniport-driver.md)します。

 

 

 





