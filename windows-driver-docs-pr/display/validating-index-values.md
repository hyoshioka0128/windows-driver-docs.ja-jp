---
title: インデックス値の検証
description: インデックス値の検証
ms.assetid: 09247df3-0c87-48cf-9c94-bda23c6b38d2
keywords:
- ユーザーモード表示ドライバー WDK Windows Vista、インデックスの検証
- インデックス値の検証 WDK 表示
- インデックス検証 WDK 表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2da094953a3d386da5eab1e636cc7981b7307729
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829238"
---
# <a name="validating-index-values"></a>インデックス値の検証


ユーザーモードの表示ドライバーは、インデックスの検証を実行するかどうかに関係なく、ハードウェアロゴテスト用に "Microsoft Windows 用に設計" できます。 ただし、無効なインデックスを渡す可能性のある Microsoft DirectX アプリケーションでドライバーが動作するようにするには、ユーザーモードの表示ドライバーでインデックスの検証を実行する必要があります。

次の項目を考慮する必要があります。

-   DirectX 8.0 および DirectX 9.0 アプリケーションは、頂点バッファーを使用してレンダリングするときに、ストライド値0を渡すことができます。 このような場合は、頂点0だけを参照する必要があります。 Stride 値は、ユーザーモードの表示ドライバーの[**setstreamsource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_setstreamsource)関数の呼び出しで、 [**D3DDDIARG\_setstreamsource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_setstreamsource)構造体の**stride**メンバーで設定されます。

-   ドライバーの[**Setstreamsourceum**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_setstreamsourceum)関数の呼び出しに、頂点データのサイズが含まれていません。 これは、 *Setstreamsourceum*の*pUMBuffer*パラメーターが指す頂点データを提供するユーザーメモリバッファーのサイズが指定されていないことを示します。

-   [**D3DDDIARG\_DRAWINDEXEDPRIMITIVE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_drawindexedprimitive)または[**D3DDDIARG\_DRAWINDEXEDPRIMITIVE2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_drawindexedprimitive2)構造体の**numvertices**メンバーが、ドライバーの[**DRAWINDEXEDPRIMITIVE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_drawindexedprimitive)または[**の呼び出しで0に設定されることはありません。DrawIndexedPrimitive2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_drawindexedprimitive2)関数。 ドライバーは、許容される最大インデックスを (NumVerticesÂ-1) に設定する必要があります。

 

 





