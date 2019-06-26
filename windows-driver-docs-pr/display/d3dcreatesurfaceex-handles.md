---
title: D3dCreateSurfaceEx ハンドル
description: D3dCreateSurfaceEx ハンドル
ms.assetid: ada78f89-422b-470d-9423-09968ae113e8
keywords:
- コンテキスト WDK の Direct3D D3dCreateSurfaceEx
- D3dCreateSurfaceEx
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0232b99cce828c8f7f0e863e79ee3a52da21352
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370154"
---
# <a name="d3dcreatesurfaceex-handles"></a>D3dCreateSurfaceEx ハンドル


## <span id="ddk_d3dcreatesurfaceex_handles_gg"></span><span id="DDK_D3DCREATESURFACEEX_HANDLES_GG"></span>


特定の状況が発生することができます[ **D3dCreateSurfaceEx** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex) 、破棄された無効の画面に対して呼び出されるようにします。 ドライバーによって単純に無視してこのケースを処理できる堅固**D3dCreateSurfaceEx**を持つビデオ メモリ サーフェイスでの呼び出し、 **fpVidMem** (のメンバー、 [ **DD\_画面\_GLOBAL** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_surface_global)構造) が 0 です。 ただし、ドライバーを入手できます、 **D3dCreateSurfaceEx**呼び出しがシステム メモリのサーフェスを持つ、 **fpVidMem**システム メモリのサーフェイスが破棄されていることを意味する 0 の値。 ドライバーでは、この画面に関連する既存のドライバー側データし解放する必要があります。

 

 





