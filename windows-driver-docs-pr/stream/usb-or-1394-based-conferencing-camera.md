---
title: USB または 1394 ベースの会議カメラ
description: USB または 1394 ベースの会議カメラ
ms.assetid: 06097803-a124-4c9b-bdb4-cfd8648bc81d
keywords:
- グラフ構成 WDK ビデオ キャプチャ、USB ベースのビデオ会議用カメラをフィルター処理します。
- グラフ構成 WDK ビデオ キャプチャ、1394 ベースのビデオ会議用カメラをフィルター処理します。
- ビデオ会議の USB ベース カメラ WDK のビデオのキャプチャ
- ビデオ会議の 1394 ベース カメラ WDK のビデオのキャプチャ
- ビデオ会議用カメラ WDK ビデオのキャプチャします。
- カメラの WDK ビデオのキャプチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c27a43b7473144cdd7440471dd12bd805f3f536a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382507"
---
# <a name="usb-or-1394-based-conferencing-camera"></a>USB または 1394 ベースの会議カメラ


ないテレビやラジオがそのチューニング機能の 1 つのビデオ ストリームを公開するキャプチャ フィルターの単純なフィルター グラフで構成されます。 USB および 1394 ベースのビデオ会議用カメラは、多くの場合、この構成を使用します。

次の図では、1394 ベースのビデオ会議カメラの使用可能なフィルター グラフ構成のいずれかを示します。

![ビデオ会議の 1394 ベース カメラの使用可能なフィルター グラフ構成のいずれかを示す図](images/conferencing-camera-1394.gif)

**注**  :カメラから単一のキャプチャのストリームは、個別のキャプチャとプレビュー ストリームを提供するユーザー モード DirectShow フィルター (Tee スマート フィルター) でレプリケートされます。 このレプリケーションは、データをコピーするミニドライバーを必要とせずに実行されます。

 

ベンダーは、UVC 仕様に準拠している場合、ミニドライバーは、USB ベースのカメラを記述する必要はありません。 Microsoft が提供、 [USB ビデオ クラス ドライバー](usb-video-class-driver.md)のような cameras します。 マイクロソフトでは、新しい USB ベースの会議カメラ ハードウェアが UVC 仕様に準拠して開発することをお勧めします。

Microsoft も用意されています。、 [USBCAMD ミニドライバー ライブラリ](usbcamd-minidriver-library.md)旧バージョンとの互換性のためです。 ただし、USBCAMD インターフェイスは廃止されていますと Microsoft は、さらに開発を廃止します。

 

 




