---
title: バージョン トークン
description: バージョン トークン
ms.assetid: e38ae148-3bb8-41b4-acdd-55bd67c24d48
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 663a895f6c234d8265e4295b6110b119a69377cf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551630"
---
# <a name="version-token"></a>バージョン トークン


## <span id="ddk_version_token_gg"></span><span id="DDK_VERSION_TOKEN_GG"></span>


バージョン トークンは、シェーダー コードのバージョン番号を示し、シェーダー コードがピクセルまたは頂点シェーダーがかどうかをドライバーに通知します。 バージョン トークンは、次のビットで構成されます。

### <a name="span-idbitsspanspan-idbitsspanbits"></a><span id="bits"></span><span id="BITS"></span>Bits

<span id="_07_00_"></span>**\[07時 00分\]** ビット 0 ~ 7 は、マイナー バージョン番号またはコードを示します。

<span id="_15_08_"></span>**\[15時 08分\]** ビット 8 ~ 15 は、メジャー バージョン番号またはコードを指定します。

<span id="_31_16_"></span>**\[31:16\]**  31 ビットの 16 ピクセルまたは頂点シェーダーのコードは、かどうかを指定します。
ピクセル シェーダーの値は 0 xffff です。
頂点シェーダーでは、値は 0 xfffe です。
## <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要件


Windows Vista および Windows オペレーティング システムの以降のバージョンで使用できます。

 

 





