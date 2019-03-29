---
title: インデックス値の検証
description: インデックス値の検証
ms.assetid: 09247df3-0c87-48cf-9c94-bda23c6b38d2
keywords:
- ユーザー モード ドライバー WDK Windows Vista では、インデックスの検証を表示します。
- WDK の表示インデックス値の検証
- インデックス検証 WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 943a6555d1ee8e514c1580dd014aa0d8fcd891b6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579038"
---
# <a name="validating-index-values"></a>インデックス値の検証


ユーザー モードのディスプレイ ドライバーは、インデックスの検証を実行するかどうかに関係なく、"設計の Microsoft Windows"ハードウェア ロゴ テストを渡すことができます。 ただし、ドライバーが無効なインデックスを渡すことがある Microsoft DirectX アプリケーションで動作するためには、ユーザー モードのディスプレイ ドライバーは、インデックスの検証を実行する必要があります。

次の項目を考慮してください。

-   DirectX の 8.0、9.0 の DirectX アプリケーションは、頂点バッファーを表示するときに、stride 値は 0 を渡すことができます。 このような状況では、0 は頂点のみを参照する必要があります。 Stride 値が設定されて、 **Stride**のメンバー、 [ **D3DDDIARG\_SETSTREAMSOURCE** ](https://msdn.microsoft.com/library/windows/hardware/ff543352)ユーザー モード ディスプレイ ドライバーへの呼び出しで構造[ **SetStreamSource** ](https://msdn.microsoft.com/library/windows/hardware/ff569660)関数。

-   ドライバーへの呼び出し[ **SetStreamSourceUM** ](https://msdn.microsoft.com/library/windows/hardware/ff569662)関数では、頂点データのサイズは含まれません。 頂点データを提供するユーザー メモリ バッファーのサイズを*pUMBuffer*パラメーターの*SetStreamSourceUM*へのポインターが指定されていません。

-   **NumVertices**のメンバー、 [ **D3DDDIARG\_DRAWINDEXEDPRIMITIVE** ](https://msdn.microsoft.com/library/windows/hardware/ff543048)または[ **D3DDDIARG\_DRAWINDEXEDPRIMITIVE2** ](https://msdn.microsoft.com/library/windows/hardware/ff543054)構造体は、ドライバーの呼び出しで 0 に設定しないでください[ **DrawIndexedPrimitive** ](https://msdn.microsoft.com/library/windows/hardware/ff556133)または[ **DrawIndexedPrimitive2** ](https://msdn.microsoft.com/library/windows/hardware/ff556135)関数。 ドライバー許容される最大のインデックスを設定する必要があります (NumVerticesÂ-1)。

 

 





