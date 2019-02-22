---
title: NIC のスイッチを管理します。
description: NIC のスイッチを管理します。
ms.assetid: EE198C8D-427B-4013-8D19-5323332A4D87
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2972ccf8272335c115c40929722024b57eefaf62
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550758"
---
# <a name="managing-nic-switches"></a>NIC のスイッチを管理します。


このセクションでは、要件とシングル ルート I/O 仮想化 (SR-IOV) をサポートするネットワーク アダプターの NIC のスイッチを管理するためのガイドラインについて説明します。 PCI Express (PCIe) 物理機能 (PF)、SR-IOV ネットワーク アダプターのミニポート ドライバーでは、アダプターで NIC スイッチを管理します。

ここでは、次のトピックについて説明します。

[NIC のスイッチの作成](creating-a-nic-switch.md)

[NIC のスイッチを削除します。](deleting-a-nic-switch.md)

[ネットワーク アダプターで NIC スイッチを列挙します。](enumerating-nic-switches-on-a-network-adapter.md)

[NIC のスイッチのパラメーターのクエリを実行します。](querying-the-parameters-of-a-nic-switch.md)

[NIC のスイッチのパラメーターを設定します。](setting-the-parameters-of-a-nic-switch.md)

ネットワーク アダプターの SR-IOV NIC スイッチの詳細については、次を参照してください。 [NIC スイッチ](nic-switches.md)します。

**注**  だけで、PF ミニポート ドライバーは、NIC スイッチなどのネットワーク アダプターのハードウェア リソースを構成できます。 ミニポート ドライバーを PCIe 仮想機能 (VF)、SR-IOV ネットワーク アダプターでは、ほとんどのアダプターのハードウェア リソースに直接アクセスできません。 詳細については、次を参照してください。[書き込み SR-IOV VF ミニポート ドライバー](writing-sr-iov-vf-miniport-drivers.md)します。

 

 

 





