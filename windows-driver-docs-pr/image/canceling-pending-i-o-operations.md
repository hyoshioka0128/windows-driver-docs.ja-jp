---
title: 保留中の I/O 操作のキャンセル
description: 保留中の I/O 操作のキャンセル
ms.assetid: 58383836-5922-4499-a73d-d17d26dd2f76
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6857b872230b60366110bcb87e5b3c91aceefdad
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840880"
---
# <a name="canceling-pending-io-operations"></a>保留中の I/O 操作のキャンセル





WIA アプリケーションでは、 **Iwiaitemextras:: CancelPendingIO**メソッド (Microsoft Windows SDK のドキュメントで説明) を使用して、wia ミニドライバーが現在処理している保留中の i/o 操作をキャンセルできます。 **Iwiaitemextras:: CancelPendingIO**メソッドは、WIA\_イベント\_\_IO イベントを使用して[**IWiaMiniDrv::d rvnotifypnpevent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvnotifypnpevent)メソッドを呼び出します。 WIA ミニドライバーは、現在のすべての i/o 操作をキャンセルし、アイドル状態に戻す必要があります。

**Iwiaitemextras:: CancelPendingIO**メソッドは、いつでも呼び出すことができます。 すべてのカーネルモードの読み取り操作または書き込み操作で[重複 i/o](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-overlapped-i-o-operations)を使用することをお勧めします。 これにより、即時取り消しを行うことができます。 予期しない遅延が発生している、またはハングしていると思われる WIA アプリケーションは、 **Iwiaitemextras:: CancelPendingIO**メソッドを呼び出して、エンドユーザーに制御を戻すことができます。

 

 




