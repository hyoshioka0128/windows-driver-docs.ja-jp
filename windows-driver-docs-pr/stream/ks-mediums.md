---
title: KS のメディア
description: KS のメディア
ms.assetid: c94c738c-66c6-491b-9157-28cccf95af4d
keywords:
- ストリーミング メディア WDK カーネル
- KSPIN_MEDIUM
- カーネルの WDK、メディアのストリーミング
- KS WDK、メディア
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2fd901b614f4809751baf801972721b370d6d50d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380119"
---
# <a name="ks-mediums"></a>KS のメディア





A *Medium*通信バスの種類を定義します。 ミニドライバーの配列へのポインターを提供することで、pin をサポートするメディアを示す[ **KSPIN\_MEDIUM** ](https://msdn.microsoft.com/library/windows/hardware/ff563538)構造、関連する[ **KSPIN\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff563533)構造体。 KSPIN\_MEDIUM 通信バス上の特定の接続を識別します。

クライアントを設定して、接続に使用するメディアを指定する、 **Medium**内のメンバー、 [ **KSPIN\_CONNECT** ](https://msdn.microsoft.com/library/windows/hardware/ff563531) への呼び出しで提供する構造体[**KsCreatePin**](https://msdn.microsoft.com/library/windows/hardware/ff561652)します。

クライアントは、メディアを使用して、フィルターまたは暗証番号 (pin) をサポートの一覧を要求、 [ **KSPROPERTY\_PIN\_メディア**](https://msdn.microsoft.com/library/windows/hardware/ff565202)プロパティ。

 

 




