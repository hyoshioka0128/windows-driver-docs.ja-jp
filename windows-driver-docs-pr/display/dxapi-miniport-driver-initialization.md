---
title: DxApi ミニポート ドライバーの初期化
description: DxApi ミニポート ドライバーの初期化
ms.assetid: 8d2bb81c-618e-43e0-9a1a-ff0ceb732d90
keywords:
- DxApi ミニポートドライバー WDK DirectDraw、初期化
- DxApi ミニポートドライバーを初期化しています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 025d92491472b598a176840d226f6cf58883f2e5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838975"
---
# <a name="dxapi-miniport-driver-initialization"></a>DxApi ミニポート ドライバーの初期化


## <span id="ddk_dxapi_miniport_driver_initialization_gg"></span><span id="DDK_DXAPI_MINIPORT_DRIVER_INITIALIZATION_GG"></span>


DxApi インターフェイスの機能を有効にするには、DirectDraw ドライバーで初期化時に次のタスクを実行する必要があります。

1.  ドライバーは、DirectDraw が追加情報を取得するために呼び出すことができる[**DD\_HALINFO**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_halinfo)構造体で、 [**Ddgetdriverinfo**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverinfo)関数を指定する必要があります。

2.  *Ddgetdriverinfo*コールバックは、指定された\_であるという guid を使用して呼び出されます。 ドライバーは、適切なコールバックとフラグが設定された、 [**DD コールバック**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_kernelcallbacks)構造の\_に入力する必要があります。 次に、ドライバーは、この構造を[**DD\_GETDRIVERINFODATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_getdriverinfodata)構造体の**lpvdata**メンバーにコピーします。

3.  *Ddgetdriverinfo*コールバックは、guid\_、指定された guid で呼び出されます。 ドライバーは、 [**Ddカーネル**](https://docs.microsoft.com/windows/desktop/api/ddkernel/ns-ddkernel-_ddkernelcaps)の構造に収まる必要があります。 次に、ドライバーは、この構造を DD\_GETDRIVERINFODATA 構造体の**Lpvdata**メンバーにコピーします。

4.  DirectDraw ランタイムは、 **MajorFunction** = IRP\_MJ\_PNP、 **minorfunction** = IRP\_、\_QUERY\_INTERFACE、 **InterfaceType** = GUID\_dxapi を使用して、ビデオポートドライバーの IOCTL ハンドラーを呼び出します。 ビデオポートドライバーはビデオミニポートドライバーの[*HwVidQueryInterface*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_query_interface)関数を呼び出し、 [**dxapi\_インターフェイス**](https://docs.microsoft.com/windows/desktop/api/dxmini/ns-dxmini-_dxapi_interface)構造に、DirectDraw が呼び出すことのできる dxapi インターフェイスコールバック関数へのポインターを格納します。 これらのコールバック関数は、[カーネルモードのビデオトランスポートのコールバック関数](kernel-mode-video-transport-callback-functions.md)に記載されています。

ビデオミニポートドライバーは、これらの関数のいずれかが呼び出されるたびにビデオミニポートドライバーに渡される、 [**Dxapi\_インターフェイス**](https://docs.microsoft.com/windows/desktop/api/dxmini/ns-dxmini-_dxapi_interface)構造の**コンテキスト**メンバーの値を指定できます。

 

 





