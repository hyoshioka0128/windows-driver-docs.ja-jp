---
title: STI コンポーネントの概要
description: STI コンポーネントの概要
ms.assetid: 30aaa622-fb86-42dc-a417-df61e0093db3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d05bb8c82a75bff2d98352b8120cb7a6250633ee
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840776"
---
# <a name="overview-of-sti-components"></a>STI コンポーネントの概要





次の図は、Microsoft STI を構成するソフトウェアコンポーネントを示しています。 図に従うと、コンポーネントの一覧が表示されます。

![microsoft sti コンポーネントを示す図](images/sticomp.png)

### <a href="" id="ddk-imaging-application-si"></a>イメージングアプリケーション

イメージングアプリケーションでは、通常、キャプチャされた静止イメージの受信、表示、および編集を行うことができます。 イメージ取得 API (TWAIN など) を呼び出すことで、イメージを取得します。 これらのユーザーは、 [ISTILLIMAGE COM インターフェイス](istillimage-com-interface.md)を使用して、それ自体を静止イメージイベントモニターに登録する必要があります。 詳細については、「[プッシュモデル対応アプリケーションの作成](creating-push-model-aware-applications.md)」を参照してください。

### <a href="" id="ddk-image-acquisition-api-si"></a>イメージ取得 API

画像取得 Api の例としては、TWAIN、ISIS、Adobe Systems の取得などがあります。 この図は、TWAIN を示しています。 ベンダーが提供する TWAIN データソースは、静止イメージデバイスと通信する、デバイス固有のオペレーティングシステム固有のコンポーネントです。

Microsoft STI では、TWAIN データソースは、IStillImage インターフェイスと[i デバイス](istidevice-com-interface.md)インターフェイスによって提供されるメソッドを呼び出します。 [](istillimage-com-interface.md) 詳細については、「[イメージ取得 api 用のデバイス固有のコンポーネントの作成](creating-device-specific-components-for-image-acquisition-apis.md)」を参照してください。

### <a href="" id="ddk-scanners-and-cameras-control-panel-si"></a>スキャナーとカメラのコントロールパネル

[スキャナーとカメラ] コントロールパネルでは、ユーザーは次の操作を実行できます。

-   インストールされている静止イメージデバイスの一覧を表示します。

-   テスト中のイメージデバイス。

-   [まだイメージデバイスに](property-sheet-pages-for-still-image-devices.md)ついて、ベンダー提供のデバイス固有のプロパティシートページによって提供される情報を表示および変更します。

-   [静止イメージデバイスイベント](still-image-device-events.md)を特定のアプリケーションに割り当てます。

### <a href="" id="ddk-still-image-event-monitor-si"></a>静止画像イベントモニタ

静止画像イベントモニタは、静止画像サーバープロセスに存在します。 これにより、すべての静止イメージデバイス (プラグアンドプレイ互換のデバイスと、ハードウェアの追加ウィザードを使用してインストールされたデバイスの両方) のデータベースが保持されます。 また、登録されたアプリケーションのデータベースとイメージデバイスイベントも保持します。

イベントモニタは、静止画像デバイスイベントを待機します。 (イメージデバイスイベントがまだ生成されていない古いドライバーでサポートされているデバイスの場合、イベントモニターはポーリングスレッドを作成します)。イベントが検出されると、イベントモニターは、ユーザーが以前にそのイベントに割り当てたアプリケーション ([スキャナーとカメラ] コントロールパネル) を起動します。 ユーザーがイベントを複数のアプリケーションに割り当てている場合、イベントモニターは、起動するアプリケーションをユーザーに要求します。 イベントがアプリケーションに割り当てられていない場合は無視されます。

静止画像イベントモニターの詳細については、Microsoft Windows SDK のドキュメントの「*静止画像*」を参照してください。

### <a href="" id="ddk-com-interfaces-for-still-image-si"></a>静止イメージ用の COM インターフェイス

Microsoft STI は、さまざまな Microsoft STI コンポーネント間で通信パスを提供する一連の COM インターフェイスを定義します。 次の COM インターフェイスが定義されています。

[IStillImage COM インターフェイス](istillimage-com-interface.md)

[I、デバイスの COM インターフェイス](istidevice-com-interface.md)

[I(米国) COM インターフェイス](istiusd-com-interface.md)

[I、Devicecontrol COM インターフェイス](istidevicecontrol-com-interface.md)

### <a href="" id="ddk-user-mode-still-image-minidrivers-si"></a>ユーザーモード静止イメージミニドライバー

ユーザーモード静止イメージミニドライバーは、デバイス固有のユーザーモードインターフェイスを適切なカーネルモードドライバーに提供する、ベンダーが提供するコンポーネントです。 これらの各ユーザーモードドライバーは、 [Ia USD COM インターフェイス](istiusd-com-interface.md)を実装する必要があります。 これらは、 [**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)、 **ReadFile**、 **WriteFile**、 [**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)の各 Win32 関数 (Microsoft Windows SDK のドキュメントで説明) を呼び出すことによって、カーネルモードドライバーと通信します。 詳細については、「[ユーザーモードでのイメージの作成ミニドライバー](creating-a-user-mode-still-image-minidriver.md)」を参照してください。

### <a href="" id="ddk-kernel-mode-still-image-drivers-si"></a>カーネルモードのイメージドライバー

カーネルモードでも、特定の種類のバスに接続されているイメージデバイスに配信するためのパッケージデータがイメージドライバーによってパッケージ化されます。 Microsoft は、USB および SCSI バスのイメージドライバーである WDM ベースのカーネルモードを提供しています。 詳細については、「[イメージデバイス用のカーネルモードドライバーへのアクセス](accessing-kernel-mode-drivers-for-still-image-devices.md)」を参照してください。

他のバスに接続されているイメージデバイスの場合、ユーザーモードミニドライバーはカーネルモードバスドライバースタックと直接通信します。

デバイスに Microsoft が提供するドライバーとの互換性がない場合、ベンダーはカーネルモードのイメージドライバーのみを提供する必要があります。

### <a href="" id="ddk-kernel-mode-bus-driver-stacks-si"></a>カーネルモードバスドライバースタック

Microsoft では、次のように、SCSI、USB、パラレル、IEEE 1394 互換、およびシリアルバスに接続されたイメージデバイスと、インフラストラクチャレッドインターフェイスに接続されているデバイスをサポートしています。

<a href="" id="devices-connected-to-scsi-and-usb-buses"></a>**SCSI および USB バスに接続されているデバイス**  
ユーザーモードドライバー[は、静止イメージデバイス用にバス固有のカーネルモードドライバーを](accessing-kernel-mode-drivers-for-still-image-devices.md)呼び出します。

<a href="" id="devices-connected-to-a-parallel-port"></a>**パラレルポートに接続されているデバイス**  
拡張機能ポート (ECP) と拡張パラレルポート (EPP) モードがサポートされています。 ベンダーが提供するカーネルモード*フィルタードライバー*は、ユーザーモードのイメージドライバーとカーネルモードバスドライバースタックの間に追加できます。 (パラレルポートドライバーの詳細については、「[並列デバイス設計ガイド](https://docs.microsoft.com/previous-versions/ff544263(v=vs.85))」と「[並列デバイスリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。 フィルタードライバーの詳細については、「[フィルタードライバー](https://docs.microsoft.com/windows-hardware/drivers/kernel/filter-drivers)」を参照してください。)

<a href="" id="devices-connected-to-an-ieee-1394-bus"></a>**IEEE 1394 バスに接続されているデバイス**  
SBP-2 プロトコルをサポートするデバイスの場合、ユーザーモードドライバーは Microsoft の SBP インターフェイスを呼び出すことができます。 それ以外の場合は、ベンダーから提供されたフィルタードライバーが必要です。

<a href="" id="devices-connected-to-a-serial-port"></a>**シリアルポートに接続されているデバイス**  
標準のシリアルポートドライバーが使用されます。 (詳細については、「[シリアルデバイスとドライバー](https://docs.microsoft.com/previous-versions/ff547451(v=vs.85))」を参照してください)。

<a href="" id="devices-connected-to-an-infrared-interface"></a>**赤外線インターフェイスに接続されているデバイス**  
ドライバーは、 **Irsock**ソフトウェアインターフェイスを呼び出すことができます (Microsoft Windows SDK のドキュメントを参照してください)。

ベンダーは、Microsoft ドライバーでサポートされていないバスのバスドライバーのみを提供する必要があります。

 

 




