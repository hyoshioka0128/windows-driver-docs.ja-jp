---
title: 2 次元の操作のサポート
description: 2 次元の操作のサポート
ms.assetid: 09611bba-5b36-4b7d-8d93-a99590eb5bbe
keywords:
- 2 次元操作 WDK DirectX 9.0
- 2D 操作 WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6505a53bf1babc51253a4be6791e432ec28848d6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350100"
---
# <a name="supporting-two-dimensional-operations"></a>2 次元の操作のサポート


## <span id="ddk_supporting_two_dimensional_operations_gg"></span><span id="DDK_SUPPORTING_TWO_DIMENSIONAL_OPERATIONS_GG"></span>


DirectX 9.0 ランタイムでは、ドライバー、ランタイムが検出したドライバーのバージョンに応じて異なる方法で 2 次元 (2 D) のピクセル コピー操作を実行するよう指示します。 DirectX 8.1 と以前のドライバーでは、共通言語ランタイムは、ドライバーの[ *DdBlt* ](https://msdn.microsoft.com/library/windows/hardware/ff549205)関数し、では、この呼び出しの同期、[コマンド ストリーム](command-stream.md)します。 DirectX 9.0 と以降のドライバーでは、ランタイムに渡す、D3DDP2OP\_BLT、D3DDP2OP\_SURFACEBLT、または D3DDP2OP\_と共に COLORFILL オペレーション コード、 [ **D3DHAL\_DP2BLT** ](https://msdn.microsoft.com/library/windows/hardware/ff545426)、 [ **D3DHAL\_DP2SURFACEBLT**](https://msdn.microsoft.com/library/windows/hardware/ff545858)、または[ **D3DHAL\_DP2COLORFILL**](https://msdn.microsoft.com/library/windows/hardware/ff545450)コマンド ストリームでそれぞれの構造体。 DirectX 9.0 と以降のドライバーは、これらの 2D 操作コードをサポートする必要があります。

場合、ランタイム、DDBLT\_DirectX 8.1 またはそれ以前のドライバーへの呼び出しで COLORFILL フラグ*DdBlt*関数は、ランタイム変換 D3DCOLOR の塗りつぶしの色が、ランタイムと同じくらいの明示的なピクセル値を入力ターゲットのサーフェス形式を認識して (これは、形式のコードがある D3DFORMAT 列挙型のコードのいずれか)。 形式が、ベンダーによって提供される、ランタイムによって認識されない場合は、ランタイムは、処理用のドライバーに直接 D3DCOLOR 塗りつぶしの色の種類を渡します。 ただし、ランタイムは明示的なピクセル値、DirectShow によって使用されますが、ドライバーに対してプライベートである場合は、特定の色形式の D3DCOLOR 塗りつぶしの色の種類に変換します。

 

 





