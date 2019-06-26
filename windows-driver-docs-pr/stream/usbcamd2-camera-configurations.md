---
title: USBCAMD2 カメラの構成
description: USBCAMD2 カメラの構成
ms.assetid: 9a0dd6f9-aefb-4134-8bd5-31420a16db4a
keywords:
- Windows 2000 カーネル ストリーミング モデル WDK、USBCAMD2 ミニドライバー ライブラリ
- ストリーミング モデル WDK Windows 2000 カーネル、USBCAMD2 ミニドライバー ライブラリ
- カーネル ストリーミング モデルの WDK、USBCAMD2 ミニドライバー ライブラリ
- WDK Windows 2000 のカーネル ストリーミング USBCAMD2 カメラの構成
- USB ベースのストリーミング カメラ WDK USBCAMD2
- カメラ WDK USBCAMD2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e050ac3c67db708feff3c1ba0983026644d9449a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373058"
---
# <a name="usbcamd2-camera-configurations"></a>USBCAMD2 カメラの構成


クライアントは、USB カメラをサポートするミニドライバー、 *stream.sys*の上端とその下位の後、次の図に示すように、USB バス ドライバーのクラス ドライバー。

![usb カメラ ミニドライバーのモデルを示す図](images/usbimdev.png)

グループの**A**ミニドライバー ライターをする必要があります、図の構成にインターフェイスを*stream.sys*クラス ドライバー、カメラ、および USB バス。 グループ**B**構成では、デバイス固有のコードが含まれる場合にのみ、ミニドライバー USBCAMD2 を使用するように記述が必要があります。 つまり、USBCAMD2 を使用する場合は、ビデオ形式、プロパティ セット、イメージの圧縮解除、および色空間変換のサポートの実装に専念できます。 USBCAMD2 ミニドライバーのライブラリへの接続を制御する、 *stream.sys*クラス ドライバーと USB バス ドライバー、カメラのミニドライバーの開発プロセスを簡略化します。

USBCAMD2 と連動するが、 *stream.sys*クラス ドライバーは、現在使用されていません、USBCAMD2 でカメラのミニドライバーの開発はスタンドアロン独自に記述するよりも簡単にできます*stream.sys*クラスまたは、AVStream ミニドライバーします。

USBCAMD2 の主な目的は、web カメラなどのストリーミング ビデオのカメラをサポートします。 ただし、USBCAMD2 USB 一括を使用して、静止カメラから送信されたイメージをキャプチャする転送パイプの割り込みのサポートも提供します。 この機能は、まだフレームをキャプチャするスナップショット機能を備えた USB カメラをサポートします。

場合は、カメラでは、主にビデオをストリーミングし、必要に応じてスナップショット機能を提供しますは USBCAMD2 ミニドライバーのみ書き込む必要があります。 ハイブリッド cameras (カメラを主に静止画像を撮影しますが、ビデオをストリーミングすることもできます) のベンダーは、まだイメージの保存をサポートするには、ストリーミングの機能と、個別の Windows Image Acquisition (WIA) 静止カメラ ドライバーをサポートするために USBCAMD2 ミニドライバーを作成します。管理。 WIA と静止画像をキャプチャするデジタル カメラのサポートの詳細については、次を参照してください。 [Windows Image Acquisition ドライバー](https://docs.microsoft.com/windows-hardware/drivers/image/windows-image-acquisition-drivers)します。

USBCAMD2 ライブラリには、アイソクロナス pipe(s)、一括 I/O pipe(s) や、割り込みパイプの組み合わせを使用してデータ ストリームを転送し、設定を制御するカメラがサポートしています。 USBCAMD2 には、次の USB パイプの構成を実装するカメラがサポートされています。

-   先頭と末尾の動画または静止フレームなどの同期情報を 1 つの isochronous パイプは、データ ストリームに埋め込まれます。 これらの種類のカメラでは、ビデオ両方と同じアイソクロナス パイプを介してフレームもを多重化したり、まだフレームとして個々 のビデオ フレームを再利用することができます。

-   登録済みのアプリケーションに対する外部トリガ イベントのシグナル通知に、割り込みパイプ追加すると、以前の構成と同じです。

-   2 つ追加すると、最初の構成と同じ I/O パイプ コントロールへの一括し、カメラからまだフレームを取得します。

-   2 つの isochronous パイプします。 1 つのパイプにデータをストリーミングして、他のパイプの開始と終了のビデオなどの同期情報を格納またはまだフレームします。 これらのカメラはビデオ両方と同じアイソクロナス パイプを介してフレームもを多重化したり、まだフレームとして個々 のビデオ フレームを再利用できます。

-   2 つの一括 I/O パイプし、省略可能な割り込みパイプ。 ビデオ 1 つの一括パイプ ストリームとその他の一括パイプ イメージを転送もします。 省略可能な割り込みパイプは、登録済みのアプリケーションに対する外部トリガ イベントの通知を通知します。

**注**   USBCAMD2 カメラを複数の代替設定を持つ 1 つの USB インターフェイスをサポートしています。 すべての代替設定は、同じ種類とパイプの数が必要です。 この情報を指定した型の配列で[ **USBCAMD\_パイプ\_Config\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/ns-usbcamdi-_pipe_config_descriptor)に渡す[ *CamConfigureEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nc-usbcamdi-pcam_configure_routine_ex)を初期化し、カメラを構成します。

 

USBCAMD2 が USB 1.1 カメラ デバイスのみをサポートし、USB 1.1 バスの最大スループットに制限は、そのため USB 1.1 デバイスは、USB 2.0 バスに接続することができます、一方 (たとえば、アイソクロナス データの転送*完全*-speed モード)。 USBCAMD2 は USB 2.0 をサポートしていません*高*-isochronous データ転送の速度のモード。 ただし、カメラでは、一括パイプのみを実装する場合、その利点がもたらされる USB 2.0 バスに接続されている一括転送の使用可能な帯域幅があります。

 

 




