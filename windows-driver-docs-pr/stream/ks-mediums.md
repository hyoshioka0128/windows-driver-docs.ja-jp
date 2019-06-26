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
ms.openlocfilehash: 291aa5d20d1bd04ae26191f304517ce6d9c4bcf9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382503"
---
# <a name="ks-mediums"></a>KS のメディア





A *Medium*通信バスの種類を定義します。 ミニドライバーの配列へのポインターを提供することで、pin をサポートするメディアを示す[ **KSPIN\_MEDIUM** ](https://docs.microsoft.com/previous-versions/ff563538(v=vs.85))構造、関連する[ **KSPIN\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kspin_descriptor)構造体。 KSPIN\_MEDIUM 通信バス上の特定の接続を識別します。

クライアントを設定して、接続に使用するメディアを指定する、 **Medium**内のメンバー、 [ **KSPIN\_CONNECT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kspin_connect) への呼び出しで提供する構造体[**KsCreatePin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kscreatepin)します。

クライアントは、メディアを使用して、フィルターまたは暗証番号 (pin) をサポートの一覧を要求、 [ **KSPROPERTY\_PIN\_メディア**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-mediums)プロパティ。

 

 




