---
title: MPEG-4
description: MPEG-4
ms.assetid: 7879acd5-39fe-46b4-a427-43e4ea52315e
keywords:
- MPEG 4 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a929a3382a37c443fecc59666a8e78680671d3b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840548"
---
# <a name="mpeg-4"></a>MPEG-4


## <span id="ddk_mpeg_4_gg"></span><span id="DDK_MPEG_4_GG"></span>


MPEG-2 は、プログレッシブスキャンのコーディングのために、263に大きく依存していました。また、4:2:0 以外のインターレースおよびカラーサンプリング形式をサポートするために、MPEG-2 でも使用されていました。 MPEG-2 をサポートするには、263と MPEG-2 をサポートする機能を使用できます。

MPEG-2 では、8ビットを超えるサンプル精度をサポートできます。 DirectX VA には、 [**DXVA\_ピクチャパラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)構造体の**bBPPminus1**メンバーを使用して、1ピクセルあたり8ビットを超えるビットをサポートするメカニズムが含まれています。

**   図形**のコーディング、オブジェクトの向き、顔のモデリング、メッシュオブジェクト、スプライトなど、MPEG 4 に最も固有な機能は DirectX VA ではサポートされていません。

 

 

 





