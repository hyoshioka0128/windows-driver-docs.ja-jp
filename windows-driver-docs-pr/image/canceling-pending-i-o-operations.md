---
title: 保留中の I/O 操作のキャンセル
description: 保留中の I/O 操作のキャンセル
ms.assetid: 58383836-5922-4499-a73d-d17d26dd2f76
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96726fe9430f8065d07e06c9fd7bf03c2b8f477f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366724"
---
# <a name="canceling-pending-io-operations"></a>保留中の I/O 操作のキャンセル





WIA アプリケーションを使用できます、 **IWiaItemExtras::CancelPendingIO**メソッド (Microsoft Windows SDK のドキュメントで説明)、保留中、WIA ミニドライバーが処理している現在の I/O 操作をキャンセルします。 **IWiaItemExtras::CancelPendingIO**メソッドの呼び出し、 [ **IWiaMiniDrv::drvNotifyPnpEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvnotifypnpevent)メソッド、WIA を\_イベント\_キャンセル\_IO イベント。 WIA ミニドライバーは、現在のすべての I/O 操作をキャンセルする必要があります、アイドル状態に戻ります。

**IWiaItemExtras::CancelPendingIO**メソッドは、いつでも呼び出すことができます。 すべてのカーネル モードが読み取りまたは書き込み操作で使用することをお勧め[重複 I/O モード](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-overlapped-i-o-operations)します。 これにより、発生する即時キャンセルできます。 予期しない遅延が発生している、またはハングするように見える WIA アプリケーションを呼び出すことができます、 **IWiaItemExtras::CancelPendingIO**しようとする、エンドユーザーに制御を返すメソッド。

 

 




