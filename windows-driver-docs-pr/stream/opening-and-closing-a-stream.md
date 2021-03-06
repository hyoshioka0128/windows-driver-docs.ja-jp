---
title: ストリームの開始と終了
description: ストリームの開始と終了
ms.assetid: a4895e99-ab2e-482e-b89f-04b01177ec03
keywords:
- ビデオ キャプチャ WDK AVStream、ストリームを開く
- ストリームを開いて、ビデオの WDK AVStream のキャプチャ
- ビデオ キャプチャ WDK AVStream、ストリームを閉じる
- ストリームを閉じる、ビデオの WDK AVStream のキャプチャ
- WDK AVStream のストリームを開く
- WDK AVStream のストリームを閉じる
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a3ee9e0e89e167b735221572e923da0464c75aa
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362607"
---
# <a name="opening-and-closing-a-stream"></a>ストリームの開始と終了


Stream クラス インターフェイスの送信、 [ **SRB\_開く\_ストリーム**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-open-stream)選択されているビデオ形式でストリームを開き、Stream クラス ミニドライバーに要求します。 SRB で渡される情報\_開く\_ストリームには、ストリームを開くとへのポインターへのポインターのインデックスが含まれています、 [ **KS\_VIDEOINFOHEADER** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_videoinfoheader)構造体。 ストリーム インデックスの配列内のストリームのインデックスに対応して[ **KS\_DATARANGE\_ビデオ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_datarange_video)ようにミニドライバーに以前の応答によって返される構造体[**SRB\_取得\_ストリーム\_情報**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-get-stream-info)要求。 SRB の処理の詳細については\_取得\_ストリーム\_についてを参照してください[Stream カテゴリ](stream-categories.md)します。

次のコード例では、ストリーム インデックスには、カーネルのストリーミング データ形式およびカーネル ストリーミング ビデオ情報ヘッダーを取得します。

```cpp
int StreamNumber = pSrb->StreamObject->StreamNumber;
PKS_DATAFORMAT_VIDEOINFOHEADER  pKSDataFormat = 
    (PKS_DATAFORMAT_VIDEOINFOHEADER) pSrb->CommandData.OpenFormat;
PKS_VIDEOINFOHEADER pVideoInfoHdrRequested = 
    &pKSDataFormat->VideoInfoHeader;
```

ミニドライバーは、要求されたストリームの形式をサポートできることを確認してください。 内容、特に、 [ **KS\_BITMAPINFOHEADER** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_bitmapinfoheader)のトリミングおよびスケーリングによって指定された情報と共に、構造を確認するか、 **一部のみ**と**rcTarget**メンバー。

デバイスのハードウェアで要求されたキャプチャのフレーム レートをサポートできないかどうか、 **AvgTimePerFrame** KS のメンバー\_VIDEOINFOHEADER、次へ常に選択されます*低い*フレーム レートご利用いただけます。 たとえば、カメラが 7 フレーム/秒 (fps) 15 fps のキャプチャのフレーム レートをサポートできるクライアント アプリケーションが 10 fps のキャプチャのフレーム レートのストリームを開こうとすると、カメラは 7 fps 物理ストリームを作成する必要があります。

70 すべての利用可能な物理フレームのキャプチャを 10 秒のキャプチャ、ミニドライバーを報告する 100 のフレームをキャプチャするには、によってうち 30 フレームが破棄された、 [ **KSPROPERTY\_DROPPEDFRAMES\_現在**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-droppedframes-current)プロパティ。

出力バッファーが DirectDraw surface ときに、特別な規則が適用されます。 ここで、 **biWidth** 、KS のメンバー\_BITMAPINFOHEADER 構造が実際には通常、ビデオ画像の幅よりも大きい先 DirectDraw surface のストライドを表します。 サーフェスのストライドは、通常、そのバイト深さを掛けた画面の幅です。 たとえば、色深度の 32 ビット/ピクセルの幅が 640 ピクセル画面、stride は、2,560 バイトになります。

要求されたイメージの幅を決定するには、次のコード例を使用します。

```cpp
if (IsRectEmpty(&pVideoInfoHdrRequested->rcTarget) {
    Width =  pVideoInfoHdrRequested->bmiHeader.biWidth;
    Height = pVideoInfoHdrRequested->bmiHeader.biHeight;
} 
else {
    Width = pVideoInfoHdrRequested->rcTarget.right − 
            pVideoInfoHdrRequested->rcTarget.left;
    Height = pVideoInfoHdrRequested->rcTarget.bottom − 
             pVideoInfoHdrRequested->rcTarget.top;
}
```

Stream クラス インターフェイスの送信、 [ **SRB\_閉じます\_ストリーム**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-close-stream)ストリームを閉じるようにミニドライバーに要求します。 ミニドライバーは、Stream クラス インターフェイスをすべての未処理のストリームされる Srb を返す必要があります。

 

 




