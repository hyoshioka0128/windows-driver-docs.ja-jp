---
title: ビデオのキャプチャ
description: ビデオのキャプチャ
ms.assetid: 0adea8fe-1669-4daf-a858-05e014f00a72
keywords:
- ビデオ キャプチャ WDK AVStream、キャプチャ プロセス
- ビデオの WDK AVStream、プロセスのキャプチャのキャプチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95a6e812fa232d2a6f8f25040e32aadb5c7274ad
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557363"
---
# <a name="capturing-video"></a>ビデオのキャプチャ


ストリームが開始すると、 **KSSTATE\_実行**状態では、キャプチャ プロセスが開始されます。 指定したフレームの間隔に基づいて、 **AvgTimePerFrame**のメンバー、 [ **KS\_VIDEOINFOHEADER** ](https://msdn.microsoft.com/library/windows/hardware/ff567700)ストリームが開かれたときに渡された構造体、ストリームを SRB を介して渡されたバッファーにイメージを転送する\_読み取り\_データ。 キャプチャされたイメージに関する追加情報が返される、 [ **KS\_フレーム\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff567645)の末尾に追加される構造体、 [ **KSSTREAM\_ヘッダー** ](https://msdn.microsoft.com/library/windows/hardware/ff567138)構造体。

次のコード例は、追加された KS を取得します。\_フレーム\_情報構造体。

```cpp
PKSSTREAM_HEADER pDataPacket = pSrb->CommandData.DataBufferArray;
PKS_FRAME_INFO pFrameInfo = (PKS_FRAME_INFO) (pDataPacket + 1); 
```

ミニドライバーは、フレームのキャプチャを削除すると、フレームなど、キャプチャされたデータに関する追加情報フィールドを設定し、極性をフィールドする必要があります。 フレーム情報は、ドライバーの作成者によって定義されるストリームの拡張機能のメンバーでは一般的に格納されます。

```cpp
*pFrameInfo = pStrmEx->FrameInfo; // Get the frame info from the minidriver-defined stream extension
```

更新するが最善の**PictureNumber**または**DropCount**のメンバー [ **KS\_フレーム\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff567645)、[ **KS\_VBI\_フレーム\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff567694)、または[ **KSPROPERTY\_DROPPEDFRAMES\_現在\_S** ](https://msdn.microsoft.com/library/windows/hardware/ff565138)への移行で、 **KSSTATE\_ACQUIRE**状態。

これらのメンバーからの移行時を更新することができます、 **KSSTATE\_ACQUIRE**状態へ、 **KSSTATE\_一時停止**状態。

更新しない**PictureNumber**または**DropCount**からの移行時、 **KSSTATE\_一時停止**状態、 **KSSTATE\_実行**状態または**KSSTATE\_実行**状態、 **KSSTATE\_一時停止**状態。

フレームを以前に削除されて、ミニドライバーでは以降の不連続性フラグを設定し、し、その内部フラグをリセットする必要があります。 次のコードでは、データの不連続性フラグの設定を示しています。

```cpp
if (pStrmEx->fDiscontinuity) {
    pDataPacket->OptionsFlags |= KSSTREAM_HEADER_OPTIONSF_DATADISCONTINUITY;
    pStrmEx->fDiscontinuity = FALSE;
}
```

最後に、ミニドライバーは、フレームのキャプチャの完了、SRB の制御を放棄する必要があります。

```cpp
CompleteStreamSRB (pSrb);
```
