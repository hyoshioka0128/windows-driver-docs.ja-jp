---
title: 深度ステンシル値のコピー
description: 深度ステンシル値のコピー
ms.assetid: b83d4e6d-5645-49ab-bbb0-c694f1410cba
keywords:
- ユーザー モードのディスプレイ ドライバー WDK Windows Vista、深度ステンシルの値のコピー
- 深度ステンシルの値のコピー
- 深度ステンシルの値の WDK の表示
- ステンシル値 WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fef10356a68cd2894deeeecf89def6796f57c359
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370254"
---
# <a name="copying-depth-stencil-values"></a>深度ステンシル値のコピー


マイクロソフトの Direct3D ランタイムが呼び出すユーザー モードのディスプレイ ドライバーの[ **Blt** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_blt)深度ステンシルをコピーする関数がシステム メモリ、ビデオ メモリの値またはその逆です。 または、ドライバーでサポートされる非透過の深度ステンシルの形式には、ドライバーとハードウェアから形式の変換に実行する必要があります (つまり、により定義されたすべての形式、 [ **D3DDDIFORMAT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ne-d3dukmdt-_d3dddiformat)列挙型を除くD3DDDIFMT\_D\*\_LOCKABLE)、またはから、次の形式のいずれか。

-   D3DDDIFMT\_D16\_LOCKABLE

-   D3DDDIFMT\_D32\_LOCKABLE

-   D3DDDIFMT\_D32F\_LOCKABLE

-   D3DDDIFMT\_S8\_LOCKABLE

ドライバーが任意のチャンネル (深さまたはステンシル)、ソース形式を破棄しますが、変換先の形式で表示されません。 ランタイムは、すべての一般的な種類のチャネルを共有しない深度ステンシルのサーフェスの間でのコピーは許可されていません。

ドライバーでは、32 ビット符号なし整数の値に、変換先に 32 ビット符号なし整数値からソースの深さの値が最初に変換します。 これらの変換の両方に対して、次の規則が適用されます。

-   ソース深さの値が浮動小数点値にクランプがかどうか\[0, 1\]が適用されると、結果を乗算して\_最大\_UINT。

-   ソースが整数で、変換先は、低精度の整数、右端の余分なビットが削除されます。

-   ソースが整数で、宛先が高い有効桁数の整数の場合は、最も右にある余分なビットが一番左の上位ビットからレプリケートされます。

-   場合は、ソースが整数では、接続先は、浮動小数点値と 32 ビット整数が浮動小数点値に変換し、結果で除算\_最大\_UINT します。

ドライバーは、特別な処理の分散が不均等深さの値を提供する必要はありません。

ドライバーは、ソース ステンシルの値を 8 ビット整数 (つまり、左側のソース ステンシル値がゼロ ドライバー パッド) に展開します。 先表現は、精度が低いを使用している場合、ドライバー変換を実行する最上位ビットを破棄する必要があります。

ユーザー モードのディスプレイ ドライバーでは、任意の subrectangles の深度ステンシルのコピーをサポートする必要があります。 ただし、ドライバーでは、深度ステンシルのコピー中に、ミラー、拡張、またはカラー キー操作を実行する必要はありません。 ポイント サンプリングは、深度ステンシルのコピー中に暗黙的に必要があります。

 

 





