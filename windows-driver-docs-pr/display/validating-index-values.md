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
ms.openlocfilehash: b7c563aaed8960f877a669b0f0445aadcc07b1de
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373553"
---
# <a name="validating-index-values"></a>インデックス値の検証


ユーザー モードのディスプレイ ドライバーは、インデックスの検証を実行するかどうかに関係なく、"設計の Microsoft Windows"ハードウェア ロゴ テストを渡すことができます。 ただし、ドライバーが無効なインデックスを渡すことがある Microsoft DirectX アプリケーションで動作するためには、ユーザー モードのディスプレイ ドライバーは、インデックスの検証を実行する必要があります。

次の項目を考慮してください。

-   DirectX の 8.0、9.0 の DirectX アプリケーションは、頂点バッファーを表示するときに、stride 値は 0 を渡すことができます。 このような状況では、0 は頂点のみを参照する必要があります。 Stride 値が設定されて、 **Stride**のメンバー、 [ **D3DDDIARG\_SETSTREAMSOURCE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_setstreamsource)ユーザー モード ディスプレイ ドライバーへの呼び出しで構造[ **SetStreamSource** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_setstreamsource)関数。

-   ドライバーへの呼び出し[ **SetStreamSourceUM** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_setstreamsourceum)関数では、頂点データのサイズは含まれません。 頂点データを提供するユーザー メモリ バッファーのサイズを*pUMBuffer*パラメーターの*SetStreamSourceUM*へのポインターが指定されていません。

-   **NumVertices**のメンバー、 [ **D3DDDIARG\_DRAWINDEXEDPRIMITIVE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_drawindexedprimitive)または[ **D3DDDIARG\_DRAWINDEXEDPRIMITIVE2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_drawindexedprimitive2)構造体は、ドライバーの呼び出しで 0 に設定しないでください[ **DrawIndexedPrimitive** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_drawindexedprimitive)または[ **DrawIndexedPrimitive2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_drawindexedprimitive2)関数。 ドライバー許容される最大のインデックスを設定する必要があります (NumVerticesÂ-1)。

 

 





