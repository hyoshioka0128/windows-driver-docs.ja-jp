---
title: USBCAMD ミニドライバー ライブラリ
description: USBCAMD ミニドライバー ライブラリ
ms.assetid: 4447bf3d-5eaa-4de7-96bb-22dae68b44eb
keywords:
- Windows 2000 カーネル ストリーミング モデル WDK、USBCAMD2 ミニドライバー ライブラリ
- ストリーミング モデル WDK Windows 2000 カーネル、USBCAMD2 ミニドライバー ライブラリ
- カーネル ストリーミング モデルの WDK、USBCAMD2 ミニドライバー ライブラリ
- WDK Windows 2000 のカーネル ストリーミング USBCAMD2 ミニドライバー ライブラリ
- USB ベースのストリーミング カメラ WDK USBCAMD2
- カメラ WDK USBCAMD2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b8227040f4b0b4655ae6de25b5331f61ebaaa02
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531742"
---
# <a name="usbcamd-minidriver-library"></a>USBCAMD ミニドライバー ライブラリ


USBCAMD2 は、ストリーミングのカメラを USB ベースのドライバーの開発を簡素化するカーネル モード ミニドライバー ライブラリです。 Stream クラスを使用して USBCAMD2 ミニドライバー ライブラリ インターフェイス (*stream.sys*) と、USB バス ドライバーのカメラのプロパティと画像処理のサポートの実装に専念できるようにします。

Microsoft は、元の USBCAMD ミニドライバー ライブラリで、Microsoft Windows 98 ドライバー開発キット (DDK) をリリースしました。 元のライブラリは、Windows Server 2003、Windows XP、および Windows 2000 Ddk、Windows Driver Kit (WDK) で USBCAMD2 に更新されました。 USBCAMD2 追加[の新機能](usbcamd2-features.md)ピンが引き続きサポートを提供する power (休止状態) などの管理と拡張のバージョンの元の Api。

Microsoft のもの提供、USBCAMD2 ミニドライバー ライブラリだけでなく、 [USB ビデオ クラス (UVC) ドライバー](usb-video-class-driver.md) USB ベースのカメラをサポートするためにします。 UVC は、USBCAMD2 で機能のスーパー セットをサポートします。 新しいすべてのハードウェア開発の UVC ドライバーを使用することをお勧めします。 ただし、UVC に準拠するハードウェアの設計を変更することはできません場合、USBCAMD2 ミニドライバーを作成する必要があります。

ミニドライバー ライブラリは、維持、USB バスでストリームに関連付けられている開始、停止、同期、およびエラー回復の問題の処理が含まれると、デバイスから、USB バスでのデータ ストリームを管理します。 USBCAMD2 は、カーネル プロパティのサポートのストリーミング、代替の USB インターフェイスの設定、およびイメージの圧縮解除を選択すると、処理などのハードウェアの特定の操作を処理するためにベンダによって実装されたコールバック関数を呼び出します。

カメラのミニドライバーが責任を負います。

-   カーネルなどのプロパティをストリーミング用のサポートを実装する[PROPSETID\_しました\_ビデオ プロシージャ アンプ](https://msdn.microsoft.com/library/windows/hardware/ff568122)と[PROPSETID\_しました\_CAMERACONTROL](https://msdn.microsoft.com/library/windows/hardware/ff567802).

-   データ ストリームが有効でありでカメラ ミニドライバーの現在または次のビデオ フレームの一部であるかどうかを決定する[ *CamProcessUSBPacketEx* ](https://msdn.microsoft.com/library/windows/hardware/ff557631)コールバック関数。

-   ストリームからビデオ フレームを抽出し、ビデオ フレームの処理を実行する前に、カメラのミニドライバーのでは、呼び出し元のアプリケーションに返されます[ *CamProcessRawVideoFrameEx* ](https://msdn.microsoft.com/library/windows/hardware/ff557625)コールバック関数。

元の USBCAMD ミニドライバー ライブラリとして Windows 98 ではサポートされて*usbcamd.sys*が Windows 2000 ではサポートされていません。 Windows 2000 で、後で、Windows Millennium Edition 以降で両方と USBCAMD2 はサポートされて*usbcamd.sysand usbcamd2.sys*します。 USBCAMD2 も USBCAMD ミニドライバーの元のライブラリは、64 ビット プラットフォームでサポートされます。

Windows 2000 以降と Windows Millennium Edition と以降のオペレーティング システムの場合は、カメラのベンダーがライブラリを使用 USBCAMD2 ミニドライバー、元のライブラリではなくカメラ ミニドライバーを開発します。

使用することができます、 *usbintel*開始点としてカメラ ミニドライバーの例です。 このサンプルは、ドライバー開発キット (DDK) および Windows XP、Windows 7 (ビルド 7600) のように、Windows Driver Kit (WDK) で使用できます。 WDK には、このサンプルをインストールする*src\\wdm\\videocap\\usbintel* (これをインストールするオプションとして選択した) 場合。

**その他のリソース**

開発者の内容を理解する必要があります[カーネル ストリーミング](kernel-streaming.md)、[ストリーミング ミニドライバー](https://msdn.microsoft.com/library/windows/hardware/ff568275)と[ビデオ キャプチャ デバイス](video-capture-devices.md)します。

USB の仕様を含むその他の開発者については、[USB-IF 開発者領域](https://go.microsoft.com/fwlink/p/?linkid=8781)を参照してください。

[全般]、またはコンシューマーは、[USB Implementers Forum](https://go.microsoft.com/fwlink/p/?linkid=8780)を参照してください。

 

 




