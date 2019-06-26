---
title: 中間ドライバーのアンロード
description: 中間ドライバーのアンロード
ms.assetid: e3c1dad4-4262-4449-8dcd-2e2f5d6c8e25
keywords:
- NDIS 中間ドライバー WDK、アンロード
- ドライバー WDK 中級レベルのネットワーク、アンロード
- アンロードの中間ドライバー
- インストールまたは WDK NDIS 中間をアンインストールした後のクリーンアップ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 142f2b798180be7577295fce8bbff87a9587c50e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382090"
---
# <a name="unloading-an-intermediate-driver"></a>中間ドライバーのアンロード





NDIS 呼び出し、 [ *MiniportDriverUnload* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_unload)中間のドライバーをアンロードする関数。 中間ドライバーで同じ操作を実行する必要があります*MiniportDriverUnload*として他のミニポート ドライバー。 呼び出しに加え、 [ **NdisMDeregisterMiniportDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismderegisterminiportdriver)関数の場合、中間のドライバーも呼び出して[ **NdisDeregisterProtocolDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisderegisterprotocoldriver). *MiniportDriverUnload*も任意のプロトコルのドライバー リソース割り当てを解除などの任意の必要なクリーンアップ操作を実行する必要があります。

中間のドライバーをアンインストールする前にクリーンアップ操作を実行する中間のドライバーが登録できる、 [ *ProtocolUninstall* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_uninstall)関数。 たとえば、中間のドライバーの下端プロトコルが必要があります、 *ProtocolUninstall*関数。 中間ドライバーではそのプロトコル エッジのリソースを解放できます*ProtocolUninstall* NDIS 呼び出される前にその*MiniportDriverUnload*関数。

ミニポート中間ドライバーは呼び出し**NdisMDeregisterMiniportDriver** 2 回、その物理デバイス インターフェイスの 1 回と、仮想デバイス インターフェイス。

 

 





