---
title: Stream のポインターの複製
description: Stream のポインターの複製
ms.assetid: bbe01f48-db86-41c9-b7b8-b48a4a295d21
keywords:
- WDK の AVStream のポインターをストリームの複製
- ストリーム ポインター WDK AVStream の複製
- WDK AVStream のストリーム ポインターを複製します。
- WDK AVStream のストリーム ポインターをコピー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6dee974f8d927e30c24ec2f7a283b02f9c2bf528
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529009"
---
# <a name="cloning-stream-pointers"></a>Stream のポインターの複製





複数のストリーム ポインターは、1 つのフレームを参照できます。 ストリーム ポインターを複製するには、呼び出す[ **KsStreamPointerClone**](https://msdn.microsoft.com/library/windows/hardware/ff567129)します。

ストリーム ポインターの結果として得られるコピーはストリーム ポインターと呼ばれます*複製*します。 複製は、親と同じである新しいストリーム ポインターです。 最初に、クローン同じフレームを参照していますが、同じロックの状態。 作成した後は、複製をその親ストリーム ポインター依存しません。

リーディング エッジやトレーリング エッジの場合は、複製の現在のストリーム ポインターを複製することができます。

複製のストリーム ポインターを追加するその特定のフレームの参照カウントをインクリメントします。 参照してください[Stream ポインターの概要](introduction-to-stream-pointers.md)参照の詳細については、カウントされます。

複製のストリーム ポインターを使用して列挙[ **KsPinGetFirstCloneStreamPointer** ](https://msdn.microsoft.com/library/windows/hardware/ff563512)と[ **KsStreamPointerGetNextClone**](https://msdn.microsoft.com/library/windows/hardware/ff567133)します。

クローン作成を呼び出して、削除するまで[ **KsStreamPointerDelete**](https://msdn.microsoft.com/library/windows/hardware/ff567130)します。 場合、ミニドライバーは、対応するフレームの参照カウント AVStream デクリメント、クローン削除します。

参照してください[AVStream DMA サービス](avstream-dma-services.md)ストリーム ポインターのクローンを使用する方法の例についてはします。

 

 




