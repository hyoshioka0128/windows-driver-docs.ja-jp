---
title: D3dCreateSurfaceEx ハンドル
description: D3dCreateSurfaceEx ハンドル
ms.assetid: ada78f89-422b-470d-9423-09968ae113e8
keywords:
- コンテキスト WDK の Direct3D D3dCreateSurfaceEx
- D3dCreateSurfaceEx
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c22e82aa19d6dcba4053f26762f4d24d329519e8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382965"
---
# <a name="d3dcreatesurfaceex-handles"></a>D3dCreateSurfaceEx ハンドル


## <span id="ddk_d3dcreatesurfaceex_handles_gg"></span><span id="DDK_D3DCREATESURFACEEX_HANDLES_GG"></span>


特定の状況が発生することができます[ **D3dCreateSurfaceEx** ](https://msdn.microsoft.com/library/windows/hardware/ff542840) 、破棄された無効の画面に対して呼び出されるようにします。 ドライバーによって単純に無視してこのケースを処理できる堅固**D3dCreateSurfaceEx**を持つビデオ メモリ サーフェイスでの呼び出し、 **fpVidMem** (のメンバー、 [ **DD\_画面\_GLOBAL** ](https://msdn.microsoft.com/library/windows/hardware/ff551726)構造) が 0 です。 ただし、ドライバーを入手できます、 **D3dCreateSurfaceEx**呼び出しがシステム メモリのサーフェスを持つ、 **fpVidMem**システム メモリのサーフェイスが破棄されていることを意味する 0 の値。 ドライバーでは、この画面に関連する既存のドライバー側データし解放する必要があります。

 

 





