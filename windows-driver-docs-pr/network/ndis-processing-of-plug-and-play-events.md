---
title: プラグ アンド プレイのイベントの NDIS 処理
description: プラグ アンド プレイのイベントの NDIS 処理
ms.assetid: 3e9ae945-4241-4c66-bdb1-b9e3466167be
keywords:
- プラグ アンド プレイ WDK NDIS ミニポート、IRP の NIC の処理
- IRP NIC WDK NDIS の処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 025b3293bf16b601675fd6fb0c7b37dcc3095f18
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557718"
---
# <a name="ndis-processing-of-plug-and-play-events"></a>プラグ アンド プレイのイベントの NDIS 処理





[関数ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff546516) NDIS およびミニポート ドライバーのペアとして、ネットワーク インターフェイス カード (NIC) が実装されています。 NDIS が nic (FDO) 機能のデバイス オブジェクトを作成するシステムに NIC を追加するときに NDIS し、後から処理すべて Irp、プラグ アンド プレイ (PnP) など、電源管理の Irp でこの FDO に渡されます。 NIC のミニポート ドライバーは、NIC の運用インターフェイスを提供します\`

次のセクションでは、NDIS が NIC に代わって PnP Irp を処理する方法について説明します。

[NIC を追加します。](adding-a-nic.md)

[NIC の開始](starting-a-nic.md)

[NIC を停止しています](stopping-a-nic.md)

[NIC を削除します。](removing-a-nic.md)

[NIC の突然の削除の処理](processing-the-surprise-removal-of-a-nic.md)

 

 





