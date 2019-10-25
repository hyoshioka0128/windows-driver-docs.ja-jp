---
title: ビデオ ミニポート ドライバーの初期化 (Windows 2000 モデル)
description: ビデオ ミニポート ドライバーの初期化 (Windows 2000 モデル)
ms.assetid: b18b5483-f11f-4533-9434-a3a4a30fb4b2
keywords:
- ビデオミニポートドライバー WDK Windows 2000、初期化
- ビデオミニポートドライバーの初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6fbc01c9133a76899893cb2e3ecc69e8af77c21e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829194"
---
# <a name="video-miniport-driver-initialization-windows-2000-model"></a>ビデオ ミニポート ドライバーの初期化 (Windows 2000 モデル)


## <span id="ddk_video_miniport_driver_initialization_windows_2000_model__gg"></span><span id="DDK_VIDEO_MINIPORT_DRIVER_INITIALIZATION_WINDOWS_2000_MODEL__GG"></span>


ビデオミニポートドライバーの初期化は、NT カーネル、 *HAL*、および PCI バスドライバーなどのコアドライバーが読み込まれ、初期化された後に発生します。 基本的なシステム初期化シーケンスは、次のように行われます。

1.  NT カーネルと HAL が読み込まれ、初期化されます。

2.  PCI バスドライバーなどのコアドライバーが読み込まれ、初期化されます。

3.  PCI バスドライバーは、それぞれの子の PCI 構成スペースから PCI リソース情報とデバイス ID とベンダー ID を取得し、この情報をシステムに報告します。

4.  PnP マネージャーがデバイス Id とベンダー Id を認識すると、i/o マネージャーは、対応するビデオミニポートドライバーとビデオポートドライバーを既知の場所から読み込みます。 PnP マネージャーが Id を認識しない場合、ミニポートドライバーの場所をユーザーに確認し、この場所から読み込みます。

5.  I/o マネージャーは、システムによって提供される2つの入力ポインターを使用して、ミニポートドライバーの[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/display/driverentry-of-video-miniport-driver)ルーチンを呼び出します。 **Driverentry**は、[**ビデオ\_HW\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_hw_initialization_data)構造を、ドライバー固有の値とアダプター固有の値 (ミニポートドライバーのその他のエントリポイントへのポインターを含む) を使用して割り当て、初期化します。 **Driverentry**は、デバイスの PCI 構成領域に記載されていないがデバイスによってデコードされたリソースである、レガシリソースも要求する必要があります。 詳細については、「[レガシリソース](claiming-legacy-resources.md)の要求」を参照してください。

6.  ミニポートドライバーの**Driverentry**関数は、 [**videoportinitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportinitialize)を呼び出します。 **Videoportinitialize**は、すべてのミニポートドライバーに共通するミニポートドライバーの初期化の側面を実行します。 たとえば、PnP 以外のドライバーの場合、 **Videoportinitialize**は、ミニポートドライバーで初期化されたビデオ\_HW\_初期化\_データ構造の一部を検証し、システムによって作成されたデバイスの一部のパブリックメンバーを初期化します。オブジェクトは、デバイスオブジェクトのデバイス拡張機能にメモリを割り当て、デバイス拡張機能に関連情報を収集して格納します。 デバイス拡張機能の詳細については、[ビデオミニポートドライバーのデバイス拡張 (Windows 2000 モデル)](video-miniport-driver-s-device-extension--windows-2000-model-.md)に関する説明を参照してください。 PnP ドライバーの場合、デバイスオブジェクト関連のアクションは後で発生します。

7.  **Videoportinitialize**が返されると、 **Driverentry**は**videoportinitialize**の戻り値を呼び出し元に戻します。 ミニポートドライバーの作成者は、 **Videoportinitialize**によって返される値について、想定しないようにする必要があります。

この時点で、システムはビデオミニポートドライバーを読み込んで初期化しました。 次の手順では、PnP マネージャーがデバイスを起動します。 詳細については、「[ビデオミニポートドライバーのデバイスを開始](starting-the-device-of-the-video-miniport-driver.md)する」を参照してください。

 

 





