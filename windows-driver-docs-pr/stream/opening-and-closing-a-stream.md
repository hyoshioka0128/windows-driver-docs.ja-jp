---
title: ストリームの開始と終了
description: ストリームの開始と終了
ms.assetid: a4895e99-ab2e-482e-b89f-04b01177ec03
keywords:
- ビデオキャプチャ WDK AVStream、開いているストリーム
- ビデオのキャプチャ WDK AVStream、オープンストリーム
- ビデオキャプチャ WDK AVStream、閉じるストリーム
- ビデオのキャプチャ WDK AVStream、閉じているストリーム
- ストリームを開いている WDK AVStream
- ストリームを閉じる WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a813eb3706ec01773261cea02d135a9bd5f9e260
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823513"
---
# <a name="opening-and-closing-a-stream"></a>ストリームの開始と終了


ストリームクラスインターフェイスは、 [**SRB\_OPEN\_stream**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-open-stream)要求をストリームクラスミニドライバーに送信し、選択したビデオ形式でストリームを開きます。 SRB\_OPEN\_ストリームに渡される情報には、開いているストリームのインデックス、および[**KS\_VIDEOINFOHEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_videoinfoheader)構造体へのポインターへのポインターが含まれます。 ストリームインデックスは、以前の[**SRB\_GET\_stream\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-get-stream-info)要求に応答して、ミニドライバーによって返される、 [ **\_\_KS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_video)の配列内のストリームのインデックスに対応しています。 \_の処理の詳細については\_ストリームの\_情報の取得」を参照してください。[ストリームのカテゴリ](stream-categories.md)を参照してください。

次のコード例では、ストリームインデックス、カーネルストリーミングデータ形式、およびカーネルストリーミングのビデオ情報ヘッダーを取得します。

```cpp
int StreamNumber = pSrb->StreamObject->StreamNumber;
PKS_DATAFORMAT_VIDEOINFOHEADER  pKSDataFormat = 
    (PKS_DATAFORMAT_VIDEOINFOHEADER) pSrb->CommandData.OpenFormat;
PKS_VIDEOINFOHEADER pVideoInfoHdrRequested = 
    &pKSDataFormat->VideoInfoHeader;
```

ミニドライバーは、要求されたストリーム形式をサポートしていることを確認する必要があります。 具体的には、 [**KS\_BITMAPINFOHEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_bitmapinfoheader)構造体の内容を、 **Rcsource**および**rcsource**メンバーによって指定されたトリミングとスケーリングの情報と共に検証する必要があります。

デバイスのハードウェアが、 **AvgTimePerFrame**メンバーの\_メンバーで要求されたキャプチャフレームレートをサポートできない場合は、使用可能*な次の*フレームレートを常に選択する必要があります。 たとえば、カメラが1秒あたりのフレーム数 (fps) と 15 fps のキャプチャフレームレートをサポートしており、クライアントアプリケーションがストリームを 10 fps のキャプチャフレームレートで開こうとした場合、カメラは 7 fps の物理ストリームを作成する必要があります。

70の使用可能な物理フレームがすべてキャプチャされている10秒のキャプチャの場合、ミニドライバーは、DROPPEDFRAMES の現在のプロパティ[ **\_\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-droppedframes-current)によってドロップされた100フレームを報告する必要があります。

出力バッファーが DirectDraw サーフェイスの場合は、特殊なルールが適用されます。 この場合、KS\_BITMAPINFOHEADER 構造体の**Biwidth**メンバーは、実際には変換先の DirectDraw サーフェイスのストライドを表します。これは通常、ビデオイメージの幅よりも大きくなります。 サーフェイスのストライドは、通常、サーフェイスの幅とそのバイト深度を乗算したものです。 たとえば、640ピクセルの幅を持ち、色深度が32ビット/ピクセルのサーフェイスの場合、stride は2560バイトになります。

要求されたイメージの幅を確認するには、次のコード例を使用します。

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

ストリームクラスインターフェイスは、ストリームを閉じるために、 [**SRB\_CLOSE\_ストリーム**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-close-stream)要求をミニドライバーに送信します。 ミニドライバーは、すべての未処理のストリーム SRBs をストリームクラスインターフェイスに返す必要があります。

 

 




