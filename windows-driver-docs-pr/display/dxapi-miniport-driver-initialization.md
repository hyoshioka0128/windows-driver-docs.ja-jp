---
title: DxApi ミニポート ドライバーの初期化
description: DxApi ミニポート ドライバーの初期化
ms.assetid: 8d2bb81c-618e-43e0-9a1a-ff0ceb732d90
keywords:
- DxApi ミニポート ドライバー WDK DirectDraw、初期化しています
- DxApi ミニポート ドライバーの初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38016e7b0eec98b4d5c0e538ef3f359a0f7b8501
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361220"
---
# <a name="dxapi-miniport-driver-initialization"></a>DxApi ミニポート ドライバーの初期化


## <span id="ddk_dxapi_miniport_driver_initialization_gg"></span><span id="DDK_DXAPI_MINIPORT_DRIVER_INITIALIZATION_GG"></span>


DxApi インターフェイスの機能を有効にするには、DirectDraw ドライバーは、初期化時に次のタスクを実行する必要があります。

1.  ドライバーを指定する必要があります、 [ **DdGetDriverInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff549404)で機能、 [ **DD\_HALINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff551627) DirectDraw できる構造体追加情報を取得する呼び出しです。

2.  *DdGetDriverInfo*の GUID を持つコールバックが呼び出される\_KernelCallbacks GUID を指定します。 ドライバーを入力する必要があります、 [ **DD\_KERNELCALLBACKS** ](https://msdn.microsoft.com/library/windows/hardware/ff551633)適切なコールバックとフラグのセットを含む構造体。 ドライバーがこの構造をコピーし、 **lpvData**のメンバー、 [ **DD\_GETDRIVERINFODATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551550)構造体。

3.  *DdGetDriverInfo* GUID を持つコールバックが呼び出される\_KernelCaps GUID を指定します。 ドライバーを入力する必要があります、 [ **DDKERNELCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff549593)構造体。 ドライバーがこの構造をコピーし、 **lpvData** 、DD のメンバー\_GETDRIVERINFODATA 構造体。

4.  DirectDraw ランタイムが呼び出すビデオ ポート ドライバー IOCTL ハンドラーで**MajorFunction** IRP を =\_MJ\_PNP、 **MinorFunction** IRP を =\_MN\_クエリ\_インターフェイス、および**InterfaceType** GUID =\_DxApi します。 ビデオ ポート ドライバーを呼び出して、ビデオのミニポート ドライバーの[ *HwVidQueryInterface* ](https://msdn.microsoft.com/library/windows/hardware/ff567358)関数を埋めるために、 [ **DXAPI\_インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff557395) DirectDraw を呼び出すことができる DxApi インターフェイスのコールバック関数へのポインターを含む構造体。 これらのコールバック関数の一覧は[カーネル モードのビデオ トランスポート コールバック関数](kernel-mode-video-transport-callback-functions.md)します。

ビデオのミニポート ドライバーに値を指定できます、**コンテキスト**のメンバー、 [ **DXAPI\_インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff557395)ビデオのミニポート ドライバーに渡される構造体これらの関数のいずれかが呼び出されるたび。

 

 





