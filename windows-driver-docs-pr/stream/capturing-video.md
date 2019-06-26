---
title: ビデオのキャプチャ
description: ビデオのキャプチャ
ms.assetid: 0adea8fe-1669-4daf-a858-05e014f00a72
keywords:
- ビデオ キャプチャ WDK AVStream、キャプチャ プロセス
- ビデオの WDK AVStream、プロセスのキャプチャのキャプチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2e5e725e594d50921ea9c081e2cbbe21420f621
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386659"
---
# <a name="capturing-video"></a>ビデオのキャプチャ


ストリームが開始すると、 **KSSTATE\_実行**状態では、キャプチャ プロセスが開始されます。 指定したフレームの間隔に基づいて、 **AvgTimePerFrame**のメンバー、 [ **KS\_VIDEOINFOHEADER** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_videoinfoheader)ストリームが開かれたときに渡された構造体、ストリームを SRB を介して渡されたバッファーにイメージを転送する\_読み取り\_データ。 キャプチャされたイメージに関する追加情報が返される、 [ **KS\_フレーム\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_frame_info)の末尾に追加される構造体、 [ **KSSTREAM\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksstream_header)構造体。

次のコード例は、追加された KS を取得します。\_フレーム\_情報構造体。

```cpp
PKSSTREAM_HEADER pDataPacket = pSrb->CommandData.DataBufferArray;
PKS_FRAME_INFO pFrameInfo = (PKS_FRAME_INFO) (pDataPacket + 1); 
```

ミニドライバーは、フレームのキャプチャを削除すると、フレームなど、キャプチャされたデータに関する追加情報フィールドを設定し、極性をフィールドする必要があります。 フレーム情報は、ドライバーの作成者によって定義されるストリームの拡張機能のメンバーでは一般的に格納されます。

```cpp
*pFrameInfo = pStrmEx->FrameInfo; // Get the frame info from the minidriver-defined stream extension
```

更新するが最善の**PictureNumber**または**DropCount**のメンバー [ **KS\_フレーム\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_frame_info)、[ **KS\_VBI\_フレーム\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_vbi_frame_info)、または[ **KSPROPERTY\_DROPPEDFRAMES\_現在\_S** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_droppedframes_current_s)への移行で、 **KSSTATE\_ACQUIRE**状態。

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
