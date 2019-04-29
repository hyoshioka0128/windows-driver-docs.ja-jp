---
title: SRB\_初期化\_完了
description: SRB\_初期化\_完了
ms.assetid: 72412ab0-226d-4bf6-af6b-98d62653e061
keywords:
- SRB_INITIALIZATION_COMPLETE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- SRB_INITIALIZATION_COMPLETE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4eaeb70035b5057b21ca60f0cf244c527bc8f91
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390856"
---
# <a name="srbinitializationcomplete"></a>SRB\_初期化\_完了


## <span id="ddk_srb_initialization_complete_ks"></span><span id="DDK_SRB_INITIALIZATION_COMPLETE_KS"></span>


クラス ドライバーでは、この要求の初期化が完了したことをミニドライバーに通知を送信します。

### <a name="comments"></a>コメント

クラスのドライバーの送信を開始できるようにミニドライバーには、この要求が完了すると、 [ **SRB\_オープン\_ストリーム**](srb-open-stream.md)要求。

ミニドライバーで、この SRB が受信したときに、ミニドライバーは、必要なレジストリ エントリを作成します。 たとえば、DirectShow フィルター可能性があります、テレビ チューナーまたは登録クロスバーを使用して、フィルターで使用するため、 [ **StreamClassRegisterFilterWithNoKSPins** ](https://msdn.microsoft.com/library/windows/hardware/ff568261)ルーチン。

 

 





