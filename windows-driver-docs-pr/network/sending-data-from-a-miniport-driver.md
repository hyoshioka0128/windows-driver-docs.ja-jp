---
title: ミニポート ドライバーからデータを送信します。
description: ミニポート ドライバーからデータを送信します。
ms.assetid: f82475ff-8d32-4448-9b19-b6fa97a93d32
keywords:
- WDK ネットワークのデータを送信します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec41f368d101e216234767a4a18aa6924feccced
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560100"
---
# <a name="sending-data-from-a-miniport-driver"></a>ミニポート ドライバーからデータを送信します。





次の図は、ミニポート ドライバーの送信操作を示しています。

![送信操作のミニポート ドライバーを示す図](images/miniportsend.png)

NDIS ミニポート ドライバーを呼び出す[ *MiniportSendNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff559440)のリンク リストによって定義されたネットワーク データを送信する関数[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体。

ミニポート ドライバーの呼び出し、 [ **NdisMSendNetBufferListsComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563668) NET のリンクの一覧を返す関数\_バッファー\_構造体のリストを返すと、上にあるドライバーには送信要求の最終的な状態です。

 

 





