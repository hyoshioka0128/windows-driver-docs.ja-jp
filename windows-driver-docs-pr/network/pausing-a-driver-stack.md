---
title: ドライバー スタックの一時停止
description: ドライバー スタックの一時停止
ms.assetid: 6c6300e9-aea6-4da3-a91a-73db6ba8ff1f
keywords:
- ドライバー スタックの WDK ネットワーク、一時停止
- 一時停止ドライバー スタックの WDK ネットワー キング
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ee227b67327fef41ab6503eb07bda8d9b54096f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382624"
---
# <a name="pausing-a-driver-stack"></a>ドライバー スタックの一時停止





NDIS は、フィルター モジュールを挿入したり、バインドの追加などの操作を完了するドライバー スタックを一時停止します。 一般に、ドライバー スタックの一時停止操作は、次のように処理されます。

1.  NDIS ドライバーに送信、PnP の一時停止イベント プロトコル。

    バインディングは、一時停止状態になります。 すべての未処理の送信要求が完了したら、プロトコル ドライバーは PnP イベントを完了します。 バインディングは、一時停止状態です。

2.  NDIS には、スタックの上部にある以降およびミニポート ドライバーに進行して、すべてのフィルター モジュールが一時停止します。

    NDIS フィルター ドライバーを呼び出してから[ *FilterPause* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_pause)関数、フィルター モジュールは、一時停止状態になります。 で未処理のすべての NDIS 返しますが、指示を受信し、すべての未処理の送信操作が完了した後、フィルター モジュールが一時停止状態になります。

3.  NDIS は、ミニポート アダプターを一時停止します。

    NDIS ミニポート ドライバーを呼び出してから[ *MiniportPause* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_pause)関数、ミニポート アダプターは一時停止状態になります。 未処理のすべての NDIS 返します兆候を受け取った後、ミニポート アダプターは一時停止状態になります。

**注**  NDIS ドライバーに一時停止要求が失敗することはできません。 発生したエラーを記録する必要があります。

 

 

 





