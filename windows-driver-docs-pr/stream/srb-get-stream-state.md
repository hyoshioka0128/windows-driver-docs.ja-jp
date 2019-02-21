---
title: SRB\_取得\_ストリーム\_状態
description: SRB\_取得\_ストリーム\_状態
ms.assetid: ea868e5e-0724-4064-bccb-85d5b6e93d89
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 225d2f870d2d5ccb7f0c1d94a73d73964ac211c0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531640"
---
# <a name="srbgetstreamstate"></a>SRB\_取得\_ストリーム\_状態


## <span id="ddk_srb_get_stream_state_ks"></span><span id="DDK_SRB_GET_STREAM_STATE_KS"></span>


クラスのドライバーでは、このストリームのストリームの状態を取得するには、この要求を送信します。 入力ストリームの状態でのミニドライバー *pSrb*-&gt;**CommandData**.**StreamState**します。 参照してください[ **KSPROPERTY\_接続\_状態**](ksproperty-connection-state.md)ストリームの状態の説明についてはします。

 

 





