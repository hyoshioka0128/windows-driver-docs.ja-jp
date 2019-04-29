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
ms.openlocfilehash: e7e81ce362d82f746476f9db8fa277cf080bf8bb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383581"
---
# <a name="unloading-an-intermediate-driver"></a>中間ドライバーのアンロード





NDIS 呼び出し、 [ *MiniportDriverUnload* ](https://msdn.microsoft.com/library/windows/hardware/ff559378)中間のドライバーをアンロードする関数。 中間ドライバーで同じ操作を実行する必要があります*MiniportDriverUnload*として他のミニポート ドライバー。 呼び出しに加え、 [ **NdisMDeregisterMiniportDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff563578)関数の場合、中間のドライバーも呼び出して[ **NdisDeregisterProtocolDriver**](https://msdn.microsoft.com/library/windows/hardware/ff561743). *MiniportDriverUnload*も任意のプロトコルのドライバー リソース割り当てを解除などの任意の必要なクリーンアップ操作を実行する必要があります。

中間のドライバーをアンインストールする前にクリーンアップ操作を実行する中間のドライバーが登録できる、 [ *ProtocolUninstall* ](https://msdn.microsoft.com/library/windows/hardware/ff570279)関数。 たとえば、中間のドライバーの下端プロトコルが必要があります、 *ProtocolUninstall*関数。 中間ドライバーではそのプロトコル エッジのリソースを解放できます*ProtocolUninstall* NDIS 呼び出される前にその*MiniportDriverUnload*関数。

ミニポート中間ドライバーは呼び出し**NdisMDeregisterMiniportDriver** 2 回、その物理デバイス インターフェイスの 1 回と、仮想デバイス インターフェイス。

 

 





