---
title: USB ビデオ クラスの実装
description: USB ビデオ クラスの実装
ms.assetid: b390d741-9ddc-4bac-bca2-73e32461c5ed
keywords:
- USB ビデオクラスドライバー WDK AVStream、実装
- ビデオクラスドライバー WDK USB、実装
- UVC ドライバー WDK AVStream、実装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad0b41a3e1121083086a4abb8e6d2cce100b0b06
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842623"
---
# <a name="usb-video-class-implementation"></a>USB ビデオ クラスの実装


Microsoft 提供の USB ビデオクラスドライバー (usbvideo .sys) は、ピン中心の AVStream ミニドライバーです。 これは、オペレーティングシステムによって列挙された、USB ビデオクラスに準拠しているデバイスインスタンスごとにフィルターファクトリを作成します。 また、ドライバーは、デバイス上の入力または出力ターミナルごとにピンファクトリを作成します。これにより、 [**Kspin\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor)構造体のデータ**フロー**メンバーが関連する値に設定されます。

USB ビデオクラスドライバーは、デバイス記述子によって報告された内部デバイストポロジを使用して、フィルター、ノード、および接続で構成されるカーネルストリーミング (KS) トポロジグラフを作成します。

USB Video クラスは、デバイスでサポートされているコントロールの数と種類に基づいて、AVStream フィルターと pin 記述子の KS オートメーションテーブルを通じて、フィルター、ピン、およびノードプロパティセットを動的に報告します。

USB ビデオクラスでは、デバイス上の各ビデオまたは静止画像データエンドポイントでサポートされているデータ形式に基づいて、対応する KS データ範囲のリストと、各 AVStream pin 記述子のデータの共通部分を報告します。 USB ビデオクラスドライバーは、[カーネルストリーミングプロキシ](https://docs.microsoft.com/windows-hardware/drivers/ddi/_stream/index)モジュールを介して情報をエクスポートします。

USB ビデオクラスドライバーは、オーディオ/ビデオストリームの同期もサポートしています。usbvideo は KS マスタークロックとして機能し、ビデオサンプルにタイムスタンプを追加します。 USB ビデオクラス仕様には、ハードウェアがクラスドライバーにタイミング情報を提供する方法の詳細が含まれています。

USB ビデオクラスと通信するには、ユーザーモードクライアントが DirectShow またはメディアファンデーションインターフェイスを呼び出します。 これらのインターフェイスは、プラグインとしてカーネルストリーミングプロキシによって定義される COM インターフェイスラッパーです。[メディアファンデーション](https://go.microsoft.com/fwlink/p/?linkid=144771)の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

 

 




