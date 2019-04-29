---
title: NDIS I/O 作業項目
description: NDIS I/O 作業項目
ms.assetid: 4f966ff3-2092-495f-863f-50f079085fa6
keywords:
- 作業項目の I/O WDK NDIS
- I/O WDK カーネル、NDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 99e9e4d95abf4be742857812787ea3e3c0afcb1b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392913"
---
# <a name="ndis-io-work-items"></a>NDIS I/O 作業項目





ドライバー キューに I/O の作業項目コールバック関数は、後で実行できます。 NDIS は IRQL でドライバーが指定したコールバック関数を呼び出す = パッシブ\_レベル。 これにより、すぐに返される現在の関数と低い IRQL で後で作業を実行するドライバーを許可することでシステムのパフォーマンスが向上します。

NDIS 6.0 以降では、ラッパー関数カーネル I/O 作業項目のルーチン[ **IoAllocateWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff548276)、 [ **IoFreeWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff549133)、[ **IoQueueWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff549466)します。 プライベートではなく[ **IO\_作業項目**](https://msdn.microsoft.com/library/windows/hardware/ff550679)構造、NDIS は、プライベート**NDIS\_IO\_WORKITEM**構造体。

NDIS 6.0 のドライバーの呼び出し、 [ **NdisAllocateIoWorkItem** ](https://msdn.microsoft.com/library/windows/hardware/ff561604)を作業項目を割り当てる関数。 NDIS ミニポート ドライバーを渡す**NdisAllocateIoWorkItem**アダプターの処理に渡されるその NDIS、 [ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数。 **NdisAllocateIoWorkItem** 、ハンドルに関連付けられたデバイス オブジェクトを取得し、デバイスにオブジェクトを渡します、 [ **IoAllocateWorkItem** ](https://msdn.microsoft.com/library/windows/hardware/ff548276)ルーチン。 フィルター ドライバー フィルター ハンドルを渡します。

**注**  プロトコル ドライバーを使用できない[ **NdisAllocateIoWorkItem** ](https://msdn.microsoft.com/library/windows/hardware/ff561604) NDIS は、デバイス オブジェクトをプロトコル ドライバーを関連付けないので。

 

NDIS ドライバー呼び出し、 [ **NdisQueueIoWorkItem** ](https://msdn.microsoft.com/library/windows/hardware/ff563775)関数作業項目をキューに登録します。 NDIS 作業項目の使用、 **CriticalWorkQueue**キューの種類。

NDIS ドライバーを呼び出す必要があります、 [ **NdisFreeIoWorkItem** ](https://msdn.microsoft.com/library/windows/hardware/ff561855)いる職場に関連付けられているリソースを解放関数項目[ **NdisAllocateIoWorkItem** ](https://msdn.microsoft.com/library/windows/hardware/ff561604)割り当てられます。

## <a name="related-topics"></a>関連トピック


[システムのワーカー スレッド](https://msdn.microsoft.com/library/windows/hardware/ff564587)

 

 






