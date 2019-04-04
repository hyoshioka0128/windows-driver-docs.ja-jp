---
title: コマンド ストリーム
description: コマンド ストリーム
ms.assetid: 125e2072-42d6-4d4b-aec9-94b40a9d493c
keywords:
- Direct3D WDK Windows 2000 の表示、操作コード
- 操作コード WDK Direct3D
- コマンド ストリーム WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8296b3045fdde44687e8469ee2466cddb5c6784
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572837"
---
# <a name="command-stream"></a>コマンド ストリーム


## <span id="ddk_command_stream_gg"></span><span id="DDK_COMMAND_STREAM_GG"></span>


呼び出しの形式で付属する手順については、ドライバー レベルで[ **D3dDrawPrimitives2**](https://msdn.microsoft.com/library/windows/hardware/ff544704)します。 入力構造[ **D3DHAL\_DRAWPRIMITIVES2DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff545957)コマンド バッファーへのポインターが含まれています。 これは、一連の[ **D3DHAL\_DP2COMMAND** ](https://msdn.microsoft.com/library/windows/hardware/ff545454)構造体。 各構造体が含まれています、 **bCommand**メンバー データの種類で次に、バッファーを指定します。 この仕様は、の形式では、 [ **D3DHAL\_DP2OPERATION** ](https://msdn.microsoft.com/library/windows/hardware/ff545678)列挙型、D3DDP2OP など\_INDEXEDTRIANGLESTRIP またはテクスチャの状態を設定する場合D3DDP2OP\_TEXTURESTAGESTATE します。

D3DHAL つまり\_DP2OPERATION 操作コードでは、何入力構造体の次のコマンド バッファーを指定します。 従う構造体の数がいずれかで指定された**wPrimitiveCount**または**wStateCount**、さらに、D3DHAL のメンバーである共用体のメンバー\_DP2COMMAND 構造体。 **WPrimitiveCount**メンバーには、表示するために、グラフィックス プリミティブの数の追跡中に、 **wStateCount**メンバーの追跡を処理する状態の変更の数。

ドライバー操作のコードを処理する方法の例は、[テクスチャの処理ステージ](processing-texture-stages.md)を参照してください。

 

 





