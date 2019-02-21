---
title: 保留中の I/O 操作のキャンセル
description: 保留中の I/O 操作のキャンセル
ms.assetid: 58383836-5922-4499-a73d-d17d26dd2f76
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 982d86395097ba9faae9e96c7df076ef38de9fd4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553487"
---
# <a name="canceling-pending-io-operations"></a>保留中の I/O 操作のキャンセル





WIA アプリケーションを使用できます、 **IWiaItemExtras::CancelPendingIO**メソッド (Microsoft Windows SDK のドキュメントで説明)、保留中、WIA ミニドライバーが処理している現在の I/O 操作をキャンセルします。 **IWiaItemExtras::CancelPendingIO**メソッドの呼び出し、 [ **IWiaMiniDrv::drvNotifyPnpEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff544998)メソッド、WIA を\_イベント\_キャンセル\_IO イベント。 WIA ミニドライバーは、現在のすべての I/O 操作をキャンセルする必要があります、アイドル状態に戻ります。

**IWiaItemExtras::CancelPendingIO**メソッドは、いつでも呼び出すことができます。 すべてのカーネル モードが読み取りまたは書き込み操作で使用することをお勧め[重複 I/O モード](https://msdn.microsoft.com/library/windows/hardware/ff546911)します。 これにより、発生する即時キャンセルできます。 予期しない遅延が発生している、またはハングするように見える WIA アプリケーションを呼び出すことができます、 **IWiaItemExtras::CancelPendingIO**しようとする、エンドユーザーに制御を返すメソッド。

 

 




