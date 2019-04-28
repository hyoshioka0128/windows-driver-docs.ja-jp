---
title: 頂点宣言における既定のテクスチャ座標
description: ディスプレイ デバイスは、プログラミング可能なピクセル シェーダーをサポートしているディスプレイ ドライバーは、頂点宣言で不足している任意のテクスチャ座標の既定値を指定する必要があります。
ms.assetid: 5e346e7e-7460-41d9-aee1-dcc72fc642c1
keywords:
- 頂点宣言 WDK DirectX 9.0
- テクスチャ座標 WDK DirectX 9.0
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: caf14ee4fca311752276948be778b710fd0fc2dc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375947"
---
# <a name="default-texture-coordinates-in-vertex-declarations"></a>頂点宣言における既定のテクスチャ座標


**このトピックには、DirectX 8.0 以降が適用されます。**

ディスプレイ デバイスは、プログラミング可能なピクセル シェーダーをサポートしているディスプレイ ドライバーは、頂点宣言で不足している任意のテクスチャ座標の既定値を指定する必要があります。 テクスチャ座標をピクセル シェーダーに渡される 4 つのコンポーネント (u、v、w、q) が必要です。 U、v、または w 成分がない場合、ハードウェアまたはドライバーは既定値はそのコンポーネントに 0 を指定する必要があります。 Q コンポーネントが不足している場合は、ハードウェアまたはドライバーはそのコンポーネントに 1 の既定値を指定する必要があります。 そのため、すべてのコンポーネントが不足している場合、(0,0,0,1) は、既定値です。 たとえば、2 D テクスチャ座標する場合は、ハードウェアまたはドライバーそれぞれ 0 と 1 に、3 番目と 4 番目のコンポーネントの既定値を提供し、3D テクスチャの座標を使用するピクセル シェーダーに送信されます。

例外を[パラメーター トークンをソース](https://msdn.microsoft.com/library/windows/hardware/ff569716)次の命令には。

`
// D3DSIO_DEF c#,f0,f1,f2,f2
`

この手順では、ソース パラメーター トークン (f\#) 32 ビットの浮動小数点数として解釈されます。

 

 





