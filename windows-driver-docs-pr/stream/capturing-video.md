---
title: ビデオのキャプチャ
description: ビデオのキャプチャ
ms.assetid: 0adea8fe-1669-4daf-a858-05e014f00a72
keywords:
- ビデオキャプチャ WDK AVStream、キャプチャプロセス
- ビデオのキャプチャ WDK AVStream、キャプチャプロセス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a52ea2a72df32566b529b5d4fbe9303c68ec355a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844735"
---
# <a name="capturing-video"></a>ビデオのキャプチャ


ストリームが**Ksk 状態\_実行**状態になると、キャプチャプロセスが開始されます。 ストリームが開かれたときに渡された AvgTimePerFrame [**VIDEOINFOHEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_videoinfoheader)構造体\_のメンバーによって指定されたフレーム間隔に基づいて、ストリームは\_SRB を介して渡されたバッファーにイメージを転送し、\_データを読み取ります。 キャプチャされたイメージに関する追加情報は、 [**Ksstream\_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)構造体の末尾に追加される[**KS\_FRAME\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_frame_info)構造体で返されます。

次のコード例では、追加された KS\_FRAME\_INFO 構造体を取得します。

```cpp
PKSSTREAM_HEADER pDataPacket = pSrb->CommandData.DataBufferArray;
PKS_FRAME_INFO pFrameInfo = (PKS_FRAME_INFO) (pDataPacket + 1); 
```

ミニドライバーは、キャプチャされたフレーム、ドロップされたフレーム、フィールド極性など、キャプチャされたデータに関する追加情報フィールドを設定する必要があります。 フレーム情報は、通常、ドライバーライターによって定義されたストリーム拡張のメンバーに格納されます。

```cpp
*pFrameInfo = pStrmEx->FrameInfo; // Get the frame info from the minidriver-defined stream extension
```

[**Ks\_frame\_info**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_frame_info)、 [**ks\_VBI\_FRAME\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_vbi_frame_info)、または ksk プロパティ\_DROPPEDFRAMES\_現在 @no_ の**PictureNumber**または**dropcount**メンバーを更新するのが最適です[ **_t_15_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_droppedframes_current_s)は、状態の**取得\_ksk 状態**に遷移しています。

これらのメンバーは、 **Ksk 状態から\_の取得**状態から**KSK 状態\_一時停止**状態に遷移したときに更新できます。

**PictureNumber**または**dropcount**を更新しないでください **。 Ksk\_状態**から**ksk 状態\_実行**状態に移行するか、または**KSK 状態\_実行**状態を**ksk 状態\_一時停止**状態に更新してください。

フレームが既に削除されている場合、ミニドライバーは不連続フラグを設定し、その内部フラグをリセットする必要があります。 次のコードは、データの不連続性フラグを設定する方法を示しています。

```cpp
if (pStrmEx->fDiscontinuity) {
    pDataPacket->OptionsFlags |= KSSTREAM_HEADER_OPTIONSF_DATADISCONTINUITY;
    pStrmEx->fDiscontinuity = FALSE;
}
```

最後に、ミニドライバーは SRB の制御を放棄し、フレームキャプチャを完了する必要があります。

```cpp
CompleteStreamSRB (pSrb);
```
