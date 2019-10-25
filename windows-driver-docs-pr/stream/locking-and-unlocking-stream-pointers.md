---
title: ストリーム ポインターのロックとロック解除
description: ストリーム ポインターのロックとロック解除
ms.assetid: 3826a5bc-4ba5-4ada-a8aa-e7bbd949187e
keywords:
- ストリームポインター WDK AVStream、ロック、ロック解除
- ロックされたストリームポインター WDK AVStream
- ロック解除されたストリームポインター WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2acb3cae2a0fbc9438242dd408df4df9d5a1db2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838045"
---
# <a name="locking-and-unlocking-stream-pointers"></a>ストリーム ポインターのロックとロック解除





各ストリームポインターはロック状態を保持します。ロックされているかロックされていません。

ロックされたストリームポインターは、キュー内のデータを参照することが保証されます。 ロックされたストリームポインターが指すデータフレームはキャンセルできません。 そのため、ミニドライバーは、ロックされたストリームポインターを保持する時間を最小限に抑える必要があります。

ロックが解除されたストリームポインターは、キュー内のデータフレームを参照することは保証されていません。 ロックが解除されたストリームポインターを保持することで、ミニドライバーはデータポインターを保持できますが、フレームをキャンセルすることはできます。

ロックが解除されたストリームポインターが指すデータにアクセスすることができます。 [**Ksstreamポインタ clone**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerclone)で指定した*Cancelcallback*ルーチンが[**ksk streamポインタ delete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerdelete)を呼び出す場合、 *cancelcallback*とそれが実行するすべてのデータアクセスを同期する必要があります。 ミニドライバーは、別のスレッドが使用しているときに、キャンセルコールバックルーチンがストリームポインターを削除しないようにする必要があります。

キャンセルコールバックルーチンが**Ksk Streamポインタ delete**を呼び出さない場合、同期は必要ない可能性があります。

ストリームポインターをロックするには、 [**Ksstreampointerlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerlock)ロックを呼び出します。 ストリームポインターのロックを解除するには、 [**Ksk streampointer unlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerunlock)を呼び出します。

IRP がキャンセルされると、AVStream は、IRP 内のフレームをポイントするロック解除されたすべてのストリームポインターのキャンセルコールバックを呼び出します。

先頭および末尾のエッジストリームポインターは、使用されていない場合にのみ、ロックを解除します。

 

 




