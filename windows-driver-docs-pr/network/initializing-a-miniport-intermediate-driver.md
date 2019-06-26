---
title: ミニポート中間ドライバーの初期化
description: ミニポート中間ドライバーの初期化
ms.assetid: b0beea1f-7374-49e9-9650-0bdb37902469
keywords:
- NDIS 中間ドライバ、WDK の初期化
- ドライバー WDK 中級レベルのネットワーク、初期化しています
- ミニポート中間ドライバーの初期化
- ミニポート中間ドライバー WDK NDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4498be2cd4df1cc5072fd28be5df05d41d7f0a3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379216"
---
# <a name="initializing-a-miniport-intermediate-driver"></a>ミニポート中間ドライバーの初期化





ミニポート中間ドライバーには、仮想デバイス用のミニポート ドライバー、プロトコル ドライバーでは、物理デバイスのミニポート ドライバーが統合されています。 ミニポート ドライバーの上層に中間のドライバーと同様にミニポート中間ドライバー機能。 このようなドライバーには、2 つの個別のドライバーとなる可能性があるパフォーマンスの低下を発生させずに、基になるミニポート ドライバーと直接通信する中間のドライバーができます。

ミニポート中間ドライバーを呼び出してその物理ミニポート ドライバーに登録する、 [ **NdisMRegisterMiniportDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterminiportdriver)ミニポート ドライバーと同様の適切なパラメーターを持つ関数です。 その仮想のミニポート ドライバーの呼び出しを登録する**NdisMRegisterMiniportDriver** NDIS がもう一度、\_中間\_ドライバー フラグの設定の構造で*MiniportDriverCharacteristics*します。

ミニポート中間ドライバーの場合は、各仮想または物理デバイス インスタンスの場合、 **IMMiniport**にレジストリ キーが設定されている**DWORD:0x0000001**、NDIS 呼び出し、 [ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)仮想デバイスのドライバーが登録されている関数。 それ以外の場合、ドライバーの呼び出す NDIS *MiniportInitializeEx*物理的なデバイス ドライバーが登録されている関数。

 

 





