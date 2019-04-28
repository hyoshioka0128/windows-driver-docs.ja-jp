---
title: USB カメラからの静止画のキャプチャ
description: USB カメラからの静止画のキャプチャ
ms.assetid: 762021ea-753c-4cd2-9eec-1403ee918d4e
keywords:
- Windows 2000 カーネル ストリーミング モデル WDK、USBCAMD2 ミニドライバー ライブラリ
- ストリーミング モデル WDK Windows 2000 カーネル、USBCAMD2 ミニドライバー ライブラリ
- カーネル ストリーミング モデルの WDK、USBCAMD2 ミニドライバー ライブラリ
- WDK Windows 2000 のカーネル ストリーミング USBCAMD2 ミニドライバー ライブラリ
- USB ベースのストリーミング カメラ WDK USBCAMD2
- カメラ WDK USBCAMD2
- まだ WDK USBCAMD2 のフレームをキャプチャします。
- フレームはまだ WDK USBCAMD2 をキャプチャします。
- 一括パイプ WDK USBCAMD2
- プッシュ モデル WDK USBCAMD2
- プル モデル WDK USBCAMD2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d991129d9d4a13bb3cbd5601259c4264b7c15cf2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370227"
---
# <a name="capturing-still-frames-from-a-usb-camera"></a>USB カメラからの静止画のキャプチャ





USBCAMD2、別の機能を提供する[静止画像ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff548278)カメラの一括パイプを介してカメラからまだフレームを取得します。

***<em>まだフレームのキャプチャをサポートするためには、USBCAMD2 ミニドライバーを次に実行する必要があります。</em>***

-   呼び出す[ *USBCAMD\_BulkReadWrite* ](https://msdn.microsoft.com/library/windows/hardware/ff568577) 、PROPSETID から\_しました\_VIDEOCONTROL プロパティ ハンドラーにミニドライバーに割り当てられたバッファーへのポインターを渡すと静止画像をキャプチャできます。 ポインターがある必要がありますいない**NULL**します。

-   USBCAMD2 を呼び出して、ミニドライバーの[ *CamNewVideoFrameEx* ](https://msdn.microsoft.com/library/windows/hardware/ff557620)一括転送を開始する前に、コールバック関数。 カメラ ミニドライバーは、実際の静止フレームが DirectShow によって割り当てられた最大サイズ未満であると判断した場合、一括転送の要求されたサイズを縮小できます。

-   一括転送が完了したら、USBCAMD2 呼び出してミニドライバーの[ *CamProcessRawVideoFrameEx* ](https://msdn.microsoft.com/library/windows/hardware/ff557625)追加処理を実行するミニドライバーを許可するコールバック関数。

使用するフレーム データ フローは、引き続き、*プル*モデル。 プルは、アプリケーションは、静止フレームを要求したときに発生します。 または、まだフレーム データ フロー内でも、*プッシュ*モデル。 プッシュは、ユーザーにプッシュ ボタン、カメラ デバイス イベントをトリガーするときに発生します。

*<strong>* 使用する、* * *</strong>プル** * * *、STI ミニドライバー * * * から取得するモデルがまだフレーム

-   カメラに関連付けられている WDM ビデオ キャプチャ ソース フィルターを開きます。

-   前の手順で取得されたフィルター ハンドルでまだ暗証番号 (pin) を開きます。

-   呼び出す**ReadFile**の最大サイズのバッファーでは、その pin。

-   一時停止から実行するように、ストリームの状態を設定します。

-   USBCAMD2 カメラ ミニドライバーのインターフェイス ポインターを取得[PROPSETID\_しました\_VIDEOCONTROL](https://msdn.microsoft.com/library/windows/hardware/ff568120)プロパティ セット。

-   設定、 *KS\_VideoControlFlag\_トリガー*に関連付けられているフラグ[ **KSPROPERTY\_VIDEOCONTROL\_モード**](https://msdn.microsoft.com/library/windows/hardware/ff566042).

*<strong>* サポートするために、* * *</strong>プッシュ** * * * を取得するモデルは、まだカメラ * からフレーム

-   渡す、 *USBCAMD\_CamControlFlag\_EnableDeviceEvents*フラグを呼び出すときに[ **USBCAMD\_InitializeNewInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff568599)からミニドライバーの SRB 内\_初期化\_デバイス ハンドラー。 ミニドライバー処理 SRB\_初期化\_内からデバイスの[ *AdapterReceivePacket* ](https://msdn.microsoft.com/library/windows/hardware/ff554080)コールバック関数。

-   USBCAMD2 送信、 [ **KSEVENT\_VIDCAPTOSTI\_EXT\_トリガー** ](https://msdn.microsoft.com/library/windows/hardware/ff561912)イベント、ユーザーに、[トリガー] ボタンをプッシュするときに、登録済みのイメージング アプリケーションをカメラ。

要求された一括読み取りまたは書き込みを取り消す場合は、アプリケーションを呼び出す必要があります**CancelIO**静止暗証番号 (pin) へのハンドルをします。 アプリケーションを呼び出す必要があります (USB 一括アウト パイプ) 経由のカメラに転送する必要があるテーブル場合、 **WriteFile**静止暗証番号 (pin) へのハンドルをします。

 

 




