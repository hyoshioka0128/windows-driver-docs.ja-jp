---
title: USB ビデオ クラスの実装
description: USB ビデオクラスの実装
ms.assetid: b390d741-9ddc-4bac-bca2-73e32461c5ed
keywords:
- USB ビデオクラスドライバー WDK AVStream、実装
- ビデオクラスドライバー WDK USB、実装
- UVC ドライバー WDK AVStream、実装
ms.date: 06/19/2020
ms.localizationpriority: medium
ms.openlocfilehash: 13e917752d6f1cf63b80b19808615c36d379dd3a
ms.sourcegitcommit: baf3075858705d4c78d4ea4b0869bf6291bcb823
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2020
ms.locfileid: "85112136"
---
# <a name="usb-video-class-implementation"></a>USB ビデオクラスの実装

Microsoft 提供の USB ビデオクラス (UVC) ドライバー (usbvideo.sys) は、pin 中心の AVStream ミニドライバーです。 これは、オペレーティングシステムによって列挙された、USB ビデオクラスに準拠しているデバイスインスタンスごとにフィルターファクトリを作成します。 また、ドライバーは、デバイス上の入力または出力ターミナルごとにピンファクトリを作成します。これにより、 [**Kspin \_ 記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor)構造体のデータ**フロー**メンバーが関連する値に設定されます。

USB ビデオクラスドライバーは、デバイス記述子によって報告された内部デバイストポロジを使用して、フィルター、ノード、および接続で構成されるカーネルストリーミング (KS) トポロジグラフを作成します。

USB Video クラスは、デバイスでサポートされているコントロールの数と種類に基づいて、AVStream フィルターと pin 記述子の KS オートメーションテーブルを通じて、フィルター、ピン、およびノードプロパティセットを動的に報告します。

USB ビデオクラスでは、デバイス上の各ビデオまたは静止画像データエンドポイントでサポートされているデータ形式に基づいて、対応する KS データ範囲のリストと、各 AVStream pin 記述子のデータの共通部分を報告します。 USB ビデオクラスドライバーは、[カーネルストリーミングプロキシ](https://docs.microsoft.com/windows-hardware/drivers/ddi/_stream/index)モジュールを介して情報をエクスポートします。

USB ビデオクラスドライバーは、オーディオ/ビデオストリームの同期もサポートしています。usbvideo.sys は、KS マスタークロックとして機能し、ビデオサンプルにタイムスタンプを追加します。 USB ビデオクラス仕様には、ハードウェアがクラスドライバーにタイミング情報を提供する方法の詳細が含まれています。

USB ビデオクラスと通信するには、ユーザーモードクライアントが DirectShow またはメディアファンデーションインターフェイスを呼び出します。 これらのインターフェイスは、プラグインとしてカーネルストリーミングプロキシによって定義される COM インターフェイスラッパーです。[メディアファンデーション](https://docs.microsoft.com/windows/win32/medfound/microsoft-media-foundation-sdk)の詳細については、Microsoft Windows SDK のドキュメントを参照してください。
