---
title: ロックおよびロック解除の Stream ポインター
description: ロックおよびロック解除の Stream ポインター
ms.assetid: 3826a5bc-4ba5-4ada-a8aa-e7bbd949187e
keywords:
- WDK AVStream、ロックおよびロック解除のポインターをストリーム配信します。
- ロックされているストリーム ポインター WDK AVStream
- ロックされていないストリーム ポインター WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a978ee693c0b381155fae20bedbb61303dd9dc9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536711"
---
# <a name="locking-and-unlocking-stream-pointers"></a>ロックおよびロック解除の Stream ポインター





各ストリーム ポインターがロックの状態を維持します。 ロックまたはロック解除のいずれか。

ストリーム ポインターをキュー内のデータを参照することが保証されますがロックされています。 ロックされているストリーム ポインターが指すデータ フレームをキャンセルできません。 ミニドライバーが費やす時間を最小限に抑え、ロックを保持するポインターをストリーム配信します。

ロックされていないストリーム ポインターは、キュー内のデータ フレームの参照は保証されません。 によってロックされていないストリーム ポインターを保持している、ミニドライバーは、データのポインターを保持がも取り消されるフレームを許可します。

ロックされていないストリーム ポインターが指すデータにアクセスすることになります。 場合、 *CancelCallback*で指定したルーチン[ **KsStreamPointerClone** ](https://msdn.microsoft.com/library/windows/hardware/ff567129)呼び出し[ **KsStreamPointerDelete**](https://msdn.microsoft.com/library/windows/hardware/ff567130)、同期する必要があります*CancelCallback*と、実行する、データにアクセスします。 ミニドライバーは、エントリの別のスレッドが使用している間、キャンセル コールバック ルーチンはストリーム ポインターが削除されないことを確認する必要があります。

キャンセル コールバック ルーチンを呼び出しません場合**KsStreamPointerDelete**同期が必要ない場合があります。

ストリーム ポインターをロックするには、呼び出す[ **KsStreamPointerLock**](https://msdn.microsoft.com/library/windows/hardware/ff567134)します。 ストリーム ポインターをロック解除するには、呼び出す[ **KsStreamPointerUnlock**](https://msdn.microsoft.com/library/windows/hardware/ff567137)します。

IRP が取り消されたときに、AVStream は IRP 内のフレームをポイントするすべてのロックされていないストリーム ポインターをキャンセル コールバックを呼び出します。

使用されていない場合にのみをリードしトレーリング エッジ ストリーム ポインターのロックを解除します。

 

 




