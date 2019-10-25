---
title: ストリーム ポインターの複製
description: ストリーム ポインターの複製
ms.assetid: bbe01f48-db86-41c9-b7b8-b48a4a295d21
keywords:
- ストリームポインター WDK AVStream、複製
- ストリームポインターの複製 WDK AVStream
- ストリームポインターの複製 WDK AVStream
- ストリームポインターのコピー WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4fd84284c4695b563d7903106e0ae8b4326b0501
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844733"
---
# <a name="cloning-stream-pointers"></a>ストリーム ポインターの複製





複数のストリームポインターが1つのフレームを参照できます。 ストリームポインターを複製するには、 [**Ksk streampointer clone**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerclone)を呼び出します。

ストリームポインターの結果のコピーは、ストリームポインターの*複製*と呼ばれます。 複製は、親と同じ新しいストリームポインターです。 最初、複製は同じフレームを参照し、同じロック状態になります。 作成された複製は、その親ストリームポインターから独立しています。

最先端のエッジ、末尾のエッジ、または現在の複製ストリームポインターを複製することができます。

複製ストリームポインターを追加すると、その特定のフレームの参照カウントがインクリメントされます。 参照カウントの詳細については、「[ストリームポインターの概要」を](introduction-to-stream-pointers.md)参照してください。

[**KsPinGetFirstCloneStreamPointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspingetfirstclonestreampointer)と[**KsStreamPointerGetNextClone**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointergetnextclone)を使用して、複製ストリームポインターを列挙します。

のクローンは、 [**Ksk Streamポインター delete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerdelete)を呼び出すことによって削除されるまで存在します。 ミニドライバーが複製を削除すると、AVStream は対応するフレームの参照カウントをデクリメントします。

ストリームポインターの複製の使用方法の例については、「 [AVSTREAM DMA サービス](avstream-dma-services.md)」を参照してください。

 

 




