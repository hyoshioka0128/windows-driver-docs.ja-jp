---
title: USBCAMD ミニドライバー ライブラリ
description: USBCAMD ミニドライバー ライブラリ
ms.assetid: 4447bf3d-5eaa-4de7-96bb-22dae68b44eb
keywords:
- Windows 2000 カーネルストリーミングモデル WDK、USBCAMD2 ミニドライバーライブラリ
- ストリーミングモデル WDK Windows 2000 カーネル、USBCAMD2 ミニドライバーライブラリ
- カーネルストリーミングモデル WDK、USBCAMD2 ミニドライバーライブラリ
- USBCAMD2 ミニドライバー library WDK Windows 2000 カーネルストリーミング
- USB ベースのストリーミングカメラの WDK USBCAMD2
- カメラ WDK USBCAMD2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b926488600223a4bcc974937304b43ed51c3926
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827367"
---
# <a name="usbcamd-minidriver-library"></a>USBCAMD ミニドライバー ライブラリ


USBCAMD2 は、USB ベースのストリーミングカメラのドライバー開発を簡素化するカーネルモードのミニドライバーライブラリです。 USBCAMD2 ミニドライバーライブラリは、ストリームクラス ( *.sys*) と USB バスドライバーを使用してインターフェイスを作成し、カメラのプロパティとイメージ処理のサポートの実装に専念できるようにします。

Microsoft は、Microsoft Windows 98 Driver Development Kit (DDK) を使用して、元の USBCAMD ミニドライバーライブラリをリリースしました。 元のライブラリは、windows Server 2003、Windows XP、および Windows 2000 DDKs および windows Driver Kit (WDK) の USBCAMD2 に更新されました。 USBCAMD2 には、引き続き pin、電源管理 (休止状態など)、および元の Api の拡張バージョンをサポートする[新機能](usbcamd2-features.md)が追加されています。

Microsoft では、USBCAMD2 ミニドライバーライブラリに加えて、usb ベースのカメラをサポートするための[Usb ビデオクラス (UVC) ドライバー](usb-video-class-driver.md)も提供しています。 UVC は、USBCAMD2 の機能のスーパーセットをサポートしています。 Microsoft では、すべての新しいハードウェア開発に UVC ドライバーを使用することをお勧めします。 ただし、ハードウェア設計を UVC 準拠に変更できない場合は、USBCAMD2 ミニドライバーを作成する必要があります。

ミニドライバーライブラリは、デバイスからの USB バス上のデータストリームを管理します。これには、USB バスでのストリームの保持に関連する開始、停止、同期、エラー回復の問題の処理が含まれます。 USBCAMD2 は、ベンダーが実装したコールバック関数を呼び出して、カーネルストリーミングプロパティのサポート、代替 USB インターフェイス設定の選択、イメージの展開と処理など、ハードウェア固有の操作を処理します。

カメラミニドライバーは次の役割を担います。

-   [Propsetid\_VIDCAP\_VIDEOPROCAMP](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-videoprocamp) 、 [PROPSETID\_VIDCAP\_CAMERACONTROL](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-cameracontrol)などのカーネルストリーミングプロパティのサポートを実装しています。

-   データストリームが有効であるかどうか、およびカメラミニドライバーの[*CamProcessUSBPacketEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_process_packet_routine_ex)コールバック関数の現在または次のビデオフレームの一部であるかどうかを確認しています。

-   カメラミニドライバーの[*CamProcessRawVideoFrameEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_process_raw_frame_routine_ex) callback 関数で、ストリームからビデオフレームを抽出し、ビデオフレームの処理を実行してから、そのビデオフレームが呼び出し元のアプリケーションに返されるようにします。

元の USBCAMD ミニドライバーライブラリは、 *USBCAMD*として windows 98 でサポートされていますが、windows 2000 ではサポートされていません。 USBCAMD2 は、 *usbcamd と USBCAMD2*の両方として、windows 2000 以降および Windows Millennium Edition 以降でサポートされています。 64ビットプラットフォームでは、元の USBCAMD ミニドライバーライブラリも USBCAMD2 もサポートされていません。

Windows 2000 以降および Windows Millennium Edition 以降のオペレーティングシステムでは、カメラベンダーは、元のライブラリの代わりに USBCAMD2 ミニドライバーライブラリを使用して、カメラミニドライバーを開発する必要があります。

出発点として、 *usbintel* example camera ミニドライバーを使用できます。 このサンプルは、Driver Development Kit (DDK) と windows XP の windows Driver Kit (WDK) windows 7 (ビルド 7600) で入手できます。 WDK は、このサンプルを*src\\wdm\\videocap\\usbintel* (インストールするオプションとして選択されている場合) にインストールします。

**その他のリソース**

開発者は、[カーネルストリーミング](kernel-streaming.md)、[ストリーミングミニドライバー](https://docs.microsoft.com/windows-hardware/drivers/ddi/_stream/index)、および[ビデオキャプチャデバイス](video-capture-devices.md)の資料を理解する必要があります。

USB 仕様など、開発者向けのその他の情報については、「 [usb (開発者](https://go.microsoft.com/fwlink/p/?linkid=8781))」の領域を参照してください。

一般情報またはコンシューマー情報については、「 [USB 実装者フォーラム](https://go.microsoft.com/fwlink/p/?linkid=8780)」を参照してください。

 

 




