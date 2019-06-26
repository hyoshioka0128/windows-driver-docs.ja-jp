---
title: USBCAMD2 の機能
description: USBCAMD2 の機能
ms.assetid: e800948a-6903-496e-9561-697ff5ccd1d7
keywords:
- Windows 2000 カーネル ストリーミング モデル WDK、USBCAMD2 ミニドライバー ライブラリ
- ストリーミング モデル WDK Windows 2000 カーネル、USBCAMD2 ミニドライバー ライブラリ
- カーネル ストリーミング モデルの WDK、USBCAMD2 ミニドライバー ライブラリ
- WDK Windows 2000 のカーネル ストリーミング USBCAMD2 を機能します。
- USB ベースのストリーミング カメラ WDK USBCAMD2
- カメラ WDK USBCAMD2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30f9a228f501881ef5cc42ebcab1360bf5c79ca2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369535"
---
# <a name="usbcamd2-features"></a>USBCAMD2 の機能


次の機能は USBCAMD2 (元の USBCAMD ミニドライバー ライブラリではこれらの機能はサポートされません) 内に存在します。

-   **される Srb のオート コンプリート**

    USBCAMD2 はされる Srb を自動的に完了できます。 元の USBCAMD カメラ ミニドライバーされる Srb を完了する必要があります。 USBCAMD2 がされる Srb を自動的に完了することを指定するには、渡す**TRUE**で、 *NeedsCompletion*パラメーターを呼び出すと[ **USBCAMD\_AdapterReceivePacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nf-usbcamdi-usbcamd_adapterreceivepacket)します。

-   **割り込み、パイプを介してハードウェアによってトリガーされたイベントのサポート**

    USBCAMD2 カメラ ミニドライバーは、割り込みパイプを介して通知される外部トリガー イベントを登録できます。 USBCAMD2 では、割り込みを処理できます。 たとえば、割り込みパイプは、スナップショット ボタンが押されたときに、カメラのミニドライバーを通知できます。 デバイス イベントのイメージ (まだ STI) アーキテクチャのイベント モニターを通知できます。 スナップショット ボタンを押して、STI 監視通知の送信し、STI プッシュ モデルを使用して、カメラの pin にまだ関連付けられている、以前に登録された STI アプリケーションを起動できます。 外部トリガー イベントを送信する USBCAMD2 を構成するには、渡す、 *USBCAMD\_CamControlFlag\_EnableDeviceEvents*フラグ、 *CamControlFlag*を呼び出すときのパラメーター[ **USBCAMD\_InitializeNewInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nf-usbcamdi-usbcamd_initializenewinterface)します。

-   **汎用 USB パイプ構成のサポート**

    USBCAMD2 は一括または転送のビデオおよび静止画像データをアイソクロナス パイプを使用するカメラをサポートします。 USBCAMD2 は、ミニドライバーを照会し、初期化中に、パイプの構成情報を動的に作成します。 元の USBCAMD ライブラリでは、数または種類が使用されるパイプの操作について、パイプの事前設定された構成と見なされます。 パイプの構成で指定する、 [ **USBCAMD\_パイプ\_Config\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/ns-usbcamdi-_pipe_config_descriptor)配列に渡す[ *CamConfigureEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nc-usbcamdi-pcam_configure_routine_ex)します。

-   **まだピン留めし、Pin のサポートのキャプチャ**

    USBCAMD2 が静止する際に pin を公開、 *stream.sys*元 USBCAMD が公開されているキャプチャの暗証番号 (pin) だけでなくクラス。 イメージング デバイスもピンのいずれか専用のパイプがあるかをまだとビデオの両方のピンを多重化する同じパイプを使用するは、静止暗証番号 (pin) を公開できます。 まだ暗証番号 (pin) を公開する、USBCAMD に静止画像データを含む、パイプを指定する\_パイプ\_Config\_記述子の配列を配列に渡す前に**CamConfigureEx**します。

-   **プラグ アンド プレイし、電源管理のサポートの強化**

    USBCAMD2 は、Windows 2000 および突然デバイスの削除など、以降のバージョンのプラグ アンド プレイのサポートを提供します。 USBCAMD2 には、Windows XP 以降のシステムの休止状態もサポートしています (休止状態のサポートがサービス パックがインストールされていない Windows 98、Windows 98 SE、または Windows 2000 に存在しない) および Windows Millennium Edition 以降。

 

 




