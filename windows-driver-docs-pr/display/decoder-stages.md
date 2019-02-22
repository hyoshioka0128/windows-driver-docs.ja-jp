---
title: デコーダーのステージ
description: デコーダーのステージ
ms.assetid: 34562b2a-9568-440d-b6ec-dbd1e5004d56
keywords:
- DirectX のビデオ アクセラレータ WDK Windows 2000 の表示、ビデオのデコード
- ビデオ アクセラレータの WDK DirectX のビデオのデコード
- VA WDK DirectX、ビデオのデコード
- ビデオの WDK DirectX va なので、デコーダーのステージのデコード
- WDK の DirectX va なので、デコーダーのステージをデコードするビデオ
- デコーダーは、WDK DirectX VA をステージします。
- 逆コサイン不連続変換 WDK DirectX VA
- IDCT WDK DirectX VA
- MCP WDK DirectX VA
- 動き補正 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c1a39d09d330a48e2ff21153c87d4af4e3d7e3b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549518"
---
# <a name="decoder-stages"></a>デコーダーのステージ


## <span id="ddk_decoder_stages_gg"></span><span id="DDK_DECODER_STAGES_GG"></span>


次の図に示すように、デコーダーのステージでは、アクセラレータの (IDCT) 部分動き補正予測 (MCP) の逆コサイン不連続変換操作を表示します。 Dct としてデータが示される\_型が実行される IDCT の種類を制御するための構文要素。

![デコーダーのステージを示す図](images/decstages.png)

 

 





