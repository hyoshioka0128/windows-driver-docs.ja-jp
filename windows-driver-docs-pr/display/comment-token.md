---
title: コメント トークン
description: コメント トークン
ms.assetid: b1e5f8c8-4d7d-49ce-876d-4a6cbccc550d
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0fb8573358d38a3a7621bfbb336dc5709f2c4a35
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574019"
---
# <a name="comment-token"></a>コメント トークン


## <span id="ddk_comment_token_gg"></span><span id="DDK_COMMENT_TOKEN_GG"></span>


コメント トークンには次のビットで構成されるコメントの長さがについて説明します。

### <a name="span-idbitsspanspan-idbitsspanbits"></a><span id="bits"></span><span id="BITS"></span>Bits

<span id="_15_00_"></span>**\[15時 00分\]** ビット 0 ~ 15 の場合、トークンがコメント トークンであることを示します。 この値は、0 xfffe です。

<span id="_30_16_"></span>**\[30:16\]** ビット 16 30 ~ Dword に続くコメントの長さを指定します。 コメントはできる最大 2 ^128 KB のビデオ メモリやシステム メモリを等しい長さの 15 の Dword。

<span id="_31_"></span>**\[31\]**  31 のビットが 0 (0x0)。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

続くコメント内のビットの Dword の 31 注は、0x1 に設定する必要はありません。

## <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要件


Windows Vista および Windows オペレーティング システムの以降のバージョンで使用できます。

 

 





