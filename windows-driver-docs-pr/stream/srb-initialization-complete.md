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
ms.openlocfilehash: 257899c40a33b83ebdf0da4b2c8114f167733e5b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377912"
---
# <a name="srbinitializationcomplete"></a>SRB\_初期化\_完了


## <span id="ddk_srb_initialization_complete_ks"></span><span id="DDK_SRB_INITIALIZATION_COMPLETE_KS"></span>


クラス ドライバーでは、この要求の初期化が完了したことをミニドライバーに通知を送信します。

### <a name="comments"></a>コメント

クラスのドライバーの送信を開始できるようにミニドライバーには、この要求が完了すると、 [ **SRB\_オープン\_ストリーム**](srb-open-stream.md)要求。

ミニドライバーで、この SRB が受信したときに、ミニドライバーは、必要なレジストリ エントリを作成します。 たとえば、DirectShow フィルター可能性があります、テレビ チューナーまたは登録クロスバーを使用して、フィルターで使用するため、 [ **StreamClassRegisterFilterWithNoKSPins** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nf-strmini-streamclassregisterfilterwithnokspins)ルーチン。

 

 





