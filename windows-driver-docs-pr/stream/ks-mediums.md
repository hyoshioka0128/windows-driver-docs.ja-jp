---
title: KS のメディア
description: KS のメディア
ms.assetid: c94c738c-66c6-491b-9157-28cccf95af4d
keywords:
- メディア WDK カーネルストリーミング
- KSPIN_MEDIUM
- カーネルストリーミング WDK、メディア
- KS WDK、メディア
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c3e6dd6a4c8a1dec4de235b6980986595035fce
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842514"
---
# <a name="ks-mediums"></a>KS のメディア





*メディア*は、通信バスの種類を定義します。 ミニドライバーは、関連する[**kspin\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor)構造内の[**KSPIN\_中**](https://docs.microsoft.com/previous-versions/ff563538(v=vs.85))構造体の配列へのポインターを提供することによって、pin がサポートするメディアを示します。 KSPIN\_メディアは、通信バス上の特定の接続を識別します。

クライアントは、 [**KsCreatePin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kscreatepin)への呼び出しで指定される[**KSPIN\_CONNECT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_connect)構造に**medium**メンバーを設定することによって、接続に使用するメディアを指定します。

クライアントは、 [**Ksk プロパティ\_pin\_メディア**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-mediums)のプロパティを使用して、フィルターまたは pin でサポートされているメディアの一覧を要求します。

 

 




