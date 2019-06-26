---
title: ストリーム ポインターのロックとロック解除
description: ストリーム ポインターのロックとロック解除
ms.assetid: 3826a5bc-4ba5-4ada-a8aa-e7bbd949187e
keywords:
- WDK AVStream、ロックおよびロック解除のポインターをストリーム配信します。
- ロックされているストリーム ポインター WDK AVStream
- ロックされていないストリーム ポインター WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c2fe8296f806855e986e6312b41e80e11bef1c2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386641"
---
# <a name="locking-and-unlocking-stream-pointers"></a>ストリーム ポインターのロックとロック解除





各ストリーム ポインターがロックの状態を維持します。 ロックまたはロック解除のいずれか。

ストリーム ポインターをキュー内のデータを参照することが保証されますがロックされています。 ロックされているストリーム ポインターが指すデータ フレームをキャンセルできません。 ミニドライバーが費やす時間を最小限に抑え、ロックを保持するポインターをストリーム配信します。

ロックされていないストリーム ポインターは、キュー内のデータ フレームの参照は保証されません。 によってロックされていないストリーム ポインターを保持している、ミニドライバーは、データのポインターを保持がも取り消されるフレームを許可します。

ロックされていないストリーム ポインターが指すデータにアクセスすることになります。 場合、 *CancelCallback*で指定したルーチン[ **KsStreamPointerClone** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerclone)呼び出し[ **KsStreamPointerDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerdelete)、同期する必要があります*CancelCallback*と、実行する、データにアクセスします。 ミニドライバーは、エントリの別のスレッドが使用している間、キャンセル コールバック ルーチンはストリーム ポインターが削除されないことを確認する必要があります。

キャンセル コールバック ルーチンを呼び出しません場合**KsStreamPointerDelete**同期が必要ない場合があります。

ストリーム ポインターをロックするには、呼び出す[ **KsStreamPointerLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerlock)します。 ストリーム ポインターをロック解除するには、呼び出す[ **KsStreamPointerUnlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerunlock)します。

IRP が取り消されたときに、AVStream は IRP 内のフレームをポイントするすべてのロックされていないストリーム ポインターをキャンセル コールバックを呼び出します。

使用されていない場合にのみをリードしトレーリング エッジ ストリーム ポインターのロックを解除します。

 

 




