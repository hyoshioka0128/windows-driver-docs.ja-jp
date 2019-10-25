---
title: USBCAMD2 の機能
description: USBCAMD2 の機能
ms.assetid: e800948a-6903-496e-9561-697ff5ccd1d7
keywords:
- Windows 2000 カーネルストリーミングモデル WDK、USBCAMD2 ミニドライバーライブラリ
- ストリーミングモデル WDK Windows 2000 カーネル、USBCAMD2 ミニドライバーライブラリ
- カーネルストリーミングモデル WDK、USBCAMD2 ミニドライバーライブラリ
- USBCAMD2 機能 WDK Windows 2000 カーネルストリーミング
- USB ベースのストリーミングカメラの WDK USBCAMD2
- カメラ WDK USBCAMD2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54d9eab21c09a27f0411e916cd3ba1c13731f014
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843223"
---
# <a name="usbcamd2-features"></a>USBCAMD2 の機能


USBCAMD2 には次の機能があります (元の USBCAMD ミニドライバーライブラリはこれらの機能をサポートしていません)。

-   **SRBs のオートコンプリート**

    USBCAMD2 は自動的に SRBs を完了できます。 SRBs を完了するために必要な元の USBCAMD カメラミニドライバー。 USBCAMD2 が自動的に SRBs を完了するように指定するには、 [**USBCAMD\_AdapterReceivePacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nf-usbcamdi-usbcamd_adapterreceivepacket)を呼び出すときに、必要な*Scompletion*パラメーターに**TRUE**を渡します。

-   **割り込みパイプを使用した、ハードウェアによってトリガーされるイベントのサポート**

    USBCAMD2 camera ミニドライバーは、割り込みパイプを介して通知される外部トリガーイベントを登録できます。 割り込みは、USBCAMD2 で処理できます。 たとえば、割り込みパイプは、[スナップショット] ボタンが押されたときにカメラミニドライバーに信号を送ることができます。 静止画像 (STI) アーキテクチャイベントモニターには、デバイスイベントの通知を受け取ることができます。 [スナップショット] ボタンを押すと、STI モニターが通知され、カメラの静止ピンに関連付けられている以前に登録された STI アプリケーションが、STI プッシュモデルを使用して起動できます。 外部トリガーイベントを送信するように USBCAMD2 を構成するには、 [**USBCAMD\_InitializeNewInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nf-usbcamdi-usbcamd_initializenewinterface)を呼び出すときに、 *CamControlFlag*パラメーターに*USBCAMD\_CamControlFlag\_enabledeviceevents*フラグを渡します。

-   **多目的 USB パイプ構成のサポート**

    USBCAMD2 は、一括またはアイソクロナスパイプを使用してビデオと静止画像データを転送するカメラをサポートしています。 USBCAMD2 は、ミニドライバーに対してクエリを実行し、初期化中にパイプ構成情報を動的に構築します。 元の USBCAMD ライブラリは、使用されるパイプの数または種類に関する事前設定されたパイプ構成情報を前提としています。 [*CamConfigureEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_configure_routine_ex)に渡す[**USBCAMD\_パイプ\_Config\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/ns-usbcamdi-_pipe_config_descriptor)配列で、パイプ構成を指定します。

-   **Pin とキャプチャのサポートを引き続きピン留めする**

    USBCAMD2 は、元の USBCAMD が公開しているキャプチャピンに加え*て、引き続きクラスに*ピンを公開できます。 静止しているピン用の専用パイプを使用するか、同じパイプを使用して静止ピンとビデオ pin の両方を多重化するデバイスのイメージを作成する場合は、静止 pin を公開できます。 静止ピンを公開するには、配列を**CamConfigureEx**に渡す前に、USBCAMD\_パイプ\_Config\_記述子配列に静止画像データを含むパイプを指定します。

-   **プラグアンドプレイと電源管理のサポートの強化**

    USBCAMD2 では、デバイスの突然の削除など、Windows 2000 以降のバージョンでのプラグアンドプレイがサポートされています。 USBCAMD2 は、Windows XP 以降のシステム休止状態もサポートしています (休止状態のサポートは、サービスパックがインストールされていない Windows 98、Windows 98 SE、Windows 2000)、および Windows Millennium Edition 以降ではサポートされていません。

 

 




