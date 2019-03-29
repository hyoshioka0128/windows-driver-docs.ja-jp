---
title: コネクションレス低い edge ドライバーの中間データの受信
description: コネクションレスの下端を含む中間ドライバーでのデータの受信
ms.assetid: 73143c2f-4127-41fc-b916-eac87521440a
keywords:
- 中間ドライバー WDK ネットワー キング、受信操作
- NDIS は、ドライバー WDK を中間、受信操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3010f683cb8233295e500ed564b2c1d1d6f458cd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582470"
---
# <a name="receiving-data-in-an-intermediate-driver-with-a-connectionless-lower-edge"></a>コネクションレスの下端を含む中間ドライバーでのデータの受信





コネクションレスの下端と中間のドライバーが必要、 [ **ProtocolReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff570267)ネットワーク データを受信する関数。

コネクションレスのミニポート ドライバーの呼び出しを基になる、 **NdisMIndicateReceiveNetBufferLists**、1 つ以上のリンクされたリストを渡すこと[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体より高いレベルのドライバーに示された構造体の所有権を放棄します。 NET を返すより高いレベルのドライバーのデータを使用すると、\_バッファー\_ミニポート ドライバーに構造体 (および指定したリソース) を一覧表示します。

コネクションレスの下端と中間のドライバーのデータの受信についての詳細については、次を参照してください。[プロトコル ドライバーの送信と受信操作](protocol-driver-send-and-receive-operations.md)します。

 

 





