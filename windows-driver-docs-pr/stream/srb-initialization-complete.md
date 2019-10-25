---
title: SRB\_の初期化\_完了
description: SRB\_の初期化\_完了
ms.assetid: 72412ab0-226d-4bf6-af6b-98d62653e061
keywords:
- SRB_INITIALIZATION_COMPLETE ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- SRB_INITIALIZATION_COMPLETE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 32907a78c00b46bbdf62ff5a8d5ef265e74c1847
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843297"
---
# <a name="srb_initialization_complete"></a>SRB\_の初期化\_完了


## <span id="ddk_srb_initialization_complete_ks"></span><span id="DDK_SRB_INITIALIZATION_COMPLETE_KS"></span>


クラスドライバーは、この要求を送信して、初期化が完了したことをミニドライバーに通知します。

### <a name="comments"></a>コメント

ミニドライバーがこの要求を完了すると、クラスドライバーは[**オープン\_ストリーム要求の SRB\_** ](srb-open-stream.md)送信を開始できます。

この SRB がミニドライバーによって受信されると、ミニドライバーは必要なレジストリエントリを作成する必要があります。 たとえば、DirectShow フィルターでは、 [**StreamClassRegisterFilterWithNoKSPins**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassregisterfilterwithnokspins)ルーチンを使用して、filtergraph で使用する TV チューナーまたはクロスバーを登録できます。

 

 





