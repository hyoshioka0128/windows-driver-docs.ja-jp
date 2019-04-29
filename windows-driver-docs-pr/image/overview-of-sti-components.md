---
title: STI コンポーネントの概要
description: STI コンポーネントの概要
ms.assetid: 30aaa622-fb86-42dc-a417-df61e0093db3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bbe34f780fcf3f153551987db0b1a21f91ca7a54
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392650"
---
# <a name="overview-of-sti-components"></a>STI コンポーネントの概要





次の図は、Microsoft STI を構成するソフトウェア コンポーネントを示しています。 次の図は、コンポーネントの一覧です。

![microsoft sti コンポーネントを示す図](images/sticomp.png)

### <a href="" id="ddk-imaging-application-si"></a>イメージング アプリケーション

イメージング アプリケーションが通常受信、表示、およびキャプチャの静止画像の編集を許可します。 TWAIN など画像を取得、API を呼び出すことでイメージを取得します。 登録が必要な自体、静止画像イベント モニターでを通じて、 [IStillImage COM インターフェイス](istillimage-com-interface.md)します。 詳細については、次を参照してください。[プッシュ モデルの対応アプリケーションを作成する](creating-push-model-aware-applications.md)します。

### <a href="" id="ddk-image-acquisition-api-si"></a>Image Acquisition API

TWAIN、イシス、および Adobe Systems の取得、イメージの取得 Api の例です。 図では、TWAIN を示します。 TWAIN のベンダーから提供されたデータ ソースは、静止画像デバイスと通信するデバイスに固有のオペレーティング システム固有のコンポーネントです。

TWAIN データ ソースがによって提供されるメソッドを呼び出して Microsoft STI、下、 [IStillImage](istillimage-com-interface.md)と[IStiDevice](istidevice-com-interface.md)インターフェイス。 詳細については、次を参照してください。[イメージの取得 Api 用の特定のデバイス コンポーネントの作成](creating-device-specific-components-for-image-acquisition-apis.md)です。

### <a href="" id="ddk-scanners-and-cameras-control-panel-si"></a>スキャナーとカメラのコントロール パネル

スキャナーとカメラのコントロール パネル、次の操作を実行できます。

-   インストールされているデバイスの静止画像の一覧を表示します。

-   まだデバイスのイメージをテストします。

-   表示および提供情報の変更によってデバイスに固有のベンダーから提供された[プロパティ シートのページには、デバイスを静止画像](property-sheet-pages-for-still-image-devices.md)します。

-   割り当てる[デバイス イベントを静止画像](still-image-device-events.md)特定のアプリケーションにします。

### <a href="" id="ddk-still-image-event-monitor-si"></a>イベント モニターを静止画像します。

静止画像イベント モニタは、静止画像サーバー プロセスに存在します。 すべての静止画像デバイス (プラグ アンド Play−compatible の両方のデバイスおよびハードウェアの追加ウィザードでインストールされているもの) のデータベースを保持します。 登録済みのアプリケーションと、まだイメージ デバイス イベントのデータベースも保持されます。

イベント モニターでは、イメージ デバイス イベントでは引き続き待機します。 (デバイスは引き続きのイメージのデバイスのイベントは生成しない古いドライバーでサポートされている、イベント モニター作成ポーリング スレッド)。イベントが検出されたときに、イベント モニターは、ユーザーが以前 (スキャナーとカメラのコントロール パネルで) 使用して、イベントに割り当てられているアプリケーションを起動します。 ユーザーは、イベントをいくつかのアプリケーションに割り当ては、イベント モニタは起動するアプリケーションをユーザーに確認します。 イベントがすべてのアプリケーションに割り当てられていない場合は無視されます。

静止画像イベント モニターの詳細については、次を参照してください。*静止画像*、Microsoft Windows SDK ドキュメント。

### <a href="" id="ddk-com-interfaces-for-still-image-si"></a>静止画像用の COM インターフェイス

Microsoft STI には、さまざまな Microsoft STI コンポーネント間の通信パスを提供する COM インターフェイスのセットを定義します。 次の COM インターフェイスが定義されています。

[IStillImage COM インターフェイス](istillimage-com-interface.md)

[IStiDevice COM インターフェイス](istidevice-com-interface.md)

[IStiUSD COM インターフェイス](istiusd-com-interface.md)

[IStiDeviceControl COM インターフェイス](istidevicecontrol-com-interface.md)

### <a href="" id="ddk-user-mode-still-image-minidrivers-si"></a>静止画像ミニドライバーのユーザー モード

ユーザー モード静止画像ミニドライバーは、適切なカーネル モード ドライバーにデバイスに固有のユーザー モード インターフェイスを提供するベンダーから提供されたコンポーネントです。 これらのユーザー モード ドライバーの各を実装する必要があります、 [IStiUSD COM インターフェイス](istiusd-com-interface.md)します。 呼び出すことによってカーネル モード ドライバーの通信が、 [ **CreateFile**](https://msdn.microsoft.com/library/windows/desktop/aa363858)、 **ReadFile**、 **WriteFile**、および[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216) (Microsoft Windows SDK のドキュメントで説明) の Win32 関数。 詳細については、次を参照してください。[ユーザー モードのままイメージ ミニドライバーを作成する](creating-a-user-mode-still-image-minidriver.md)します。

### <a href="" id="ddk-kernel-mode-still-image-drivers-si"></a>静止画像のカーネル モード ドライバー

静止画像のカーネル モード ドライバーは、まだ特定のバスの種類に接続されているイメージのデバイスに配信するためのデータをパッケージ化します。 Microsoft では、WDM ベースのカーネル モードもイメージのドライバー USB と SCSI バス。 詳細については、次を参照してください。[静止画像デバイスへのアクセスのカーネル モードのドライバー](accessing-kernel-mode-drivers-for-still-image-devices.md)します。

画像デバイスもの他のバスに接続されている場合、ユーザー モード ミニドライバーは直接通信はカーネル モードのバス ドライバー スタックとします。

仕入先のみ、デバイスが Microsoft から提供されたドライバーと互換性がない場合は、カーネル モードの静止イメージ ドライバーを提供する必要があります。

### <a href="" id="ddk-kernel-mode-bus-driver-stacks-si"></a>カーネル モード バス ドライバー スタック

まだ SCSI、USB、並列では、次のように赤のインフラのインターフェイスに接続されているデバイスと、IEEE 1394 と互換性のあると順次のバスに接続されているイメージのデバイスで Microsoft がサポートされています。

<a href="" id="devices-connected-to-scsi-and-usb-buses"></a>**SCSI と USB バスに接続されているデバイス**  
ユーザー モード ドライバー呼び出す bus 固有[のカーネル モード ドライバーは、デバイスを静止画像](accessing-kernel-mode-drivers-for-still-image-devices.md)します。

<a href="" id="devices-connected-to-a-parallel-port"></a>**パラレル ポートに接続されているデバイス**  
拡張機能ポート (ECP) と、強化されたパラレル ポート (EPP) モードがサポートされています。 ベンダーから提供されたカーネル モード*フィルター ドライバー*静止のイメージのユーザー モード ドライバーとカーネル モードのバス ドライバー スタックとの間に追加することができます。 (パラレル ポート ドライバーの詳細については、次を参照してください。[並列のデバイス デザイン ガイド](https://msdn.microsoft.com/library/windows/hardware/ff544263)と[並列デバイス参照](https://msdn.microsoft.com/library/windows/hardware/ff544269)します。 フィルター ドライバーの詳細については、次を参照してください[フィルター ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff545890)。)。

<a href="" id="devices-connected-to-an-ieee-1394-bus"></a>**IEEE 1394 バスに接続されているデバイス**  
デバイス sbp-2 プロトコルをサポートしている場合、ユーザー モード ドライバーは Microsoft の sbp-2 インターフェイスを呼び出すことができます。 それ以外の場合、フィルターのベンダーから提供されたドライバーが必要です。

<a href="" id="devices-connected-to-a-serial-port"></a>**シリアル ポートに接続されているデバイス**  
標準のシリアル ポートのドライバーが使用されます。 (詳細については、次を参照してください[シリアル デバイスとドライバー](https://msdn.microsoft.com/library/windows/hardware/ff547451)。)。

<a href="" id="devices-connected-to-an-infrared-interface"></a>**赤外線のインターフェイスに接続されているデバイス**  
ドライバーを呼び出すことができます、 **IrSock**ソフトウェア インターフェイスが (Microsoft Windows SDK のドキュメントで説明)。

仕入先のみ、Microsoft ドライバーでサポートされていないバスのバス ドライバーを提供する必要があります。

 

 




