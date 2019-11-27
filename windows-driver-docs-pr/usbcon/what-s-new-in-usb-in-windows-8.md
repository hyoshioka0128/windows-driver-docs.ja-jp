---
Description: このトピックでは、Windows 8 でのユニバーサルシリアルバス (USB) クライアントドライバーの新機能と機能強化について説明します。
title: Windows 8-USB の新機能
ms.date: 05/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 07a2d74f9ceab7847a6ecc476e0ba887ff50a431
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843585"
---
# <a name="windows8-whats-new-for-usb"></a>Windows 8: USB の新機能


このトピックでは、Windows 8 でのユニバーサルシリアルバス (USB) クライアントドライバーの新機能と機能強化について説明します。

-   [USB 3.0 デバイスの新しいドライバースタック](#new-driver-stack-for-usb-30-devices)
-   [新しいスタックでサポートされる機能](#features-supported-by-the-new-stack)
-   [USB クライアントドライバーのクライアントコントラクトのバージョン](#client-contract-version-for-usb-client-drivers)
-   [URBs を割り当てて構築するための新しいルーチン](#new-routines-for-allocating-and-building-urbs)
-   [USB 3.0 ハブの新しいユーザーモード i/o 制御要求](#new-user-mode-io-control-requests-for-usb-30-hubs)
-   [WinUSB 用の新しい互換性 ID](#new-compatible-id-for-winusb)
-   [USB クライアントドライバー用の新しい Visual Studio テンプレート *(ベータ版の\*)* ](#new-visual-studio-templates-for-usb-client-drivers-new-for-beta)
-   [UASP ドライバー](#uasp-driver)
-   [ブートのサポート](#boot-support)
-   [強化されたデバッグ機能と診断機能](#enhanced-debugging-and-diagnostic-capabilities)
-   [デバイスマネージャーの新しい USB 固有のエラーメッセージ](#new-usb-specific-failure-messages-in-device-manager)

USB の新機能の概要については、「 [Usb ドライバーの新](https://docs.microsoft.com/windows-hardware/drivers/what-s-new-in-driver-development)機能」を参照してください。

## <a name="new-driver-stack-for-usb-30-devices"></a>USB 3.0 デバイスの新しいドライバースタック


Windows 8 には、USB 3.0 デバイスをサポートする新しい USB ドライバースタックが用意されています。 新しいスタックには、USB 3.0 デバイスが xHCI ホストコントローラーに接続されているときに Windows によって読み込まれるドライバーが含まれています。 新しいドライバーは、[カーネルモードドライバーフレームワーク](https://docs.microsoft.com/windows-hardware/drivers/what-s-new-in-driver-development)(kmdf) に基づいており、USB 3.0 仕様で定義されている機能を実装しています。 新しいドライバーは次のとおりです。

-   Usbxhci
-   Ucx01000
-   Usbhub3

新しいドライバースタックは、以前のバージョンの Windows オペレーティングシステムでビルドおよびテストされた既存のクライアントドライバーとの互換性を維持します。

USB ドライバースタックのアーキテクチャブロック図と、新しいドライバーの簡単な説明については、「 [usb 3.0 ドライバースタックアーキテクチャ](usb-3-0-driver-stack-architecture.md)」を参照してください。

## <a name="features-supported-by-the-new-stack"></a>新しいスタックでサポートされる機能


Usb 3.0 デバイスの USB ドライバースタックでは、多くの新機能がサポートされています。 一部の機能は、クライアントドライバーで構成できます。 これらの機能は次のとおりです。

-   バルクエンドポイントの静的ストリーム。

    ストリームを使用すると、クライアントドライバーは、1つの一括エンドポイントに対して複数のデータ転送を実行できます。 Windows 8 用の Windows Driver Kit (WDK) は、クライアントドライバーが一括エンドポイントで最大255のストリームを開けるようにする新しいデバイスドライバーインターフェイス (DDIs) を提供します。 ストリームが開かれると、クライアントドライバーは特定のストリームとの間でデータ転送を実行できます。 詳細については、「 [USB 一括エンドポイントで静的ストリームを開いて閉じる方法](how-to-open-streams-in-a-usb-endpoint.md)」を参照してください。

-   チェーン MDLs

    クライアントドライバーは、連続するバッファーではなく、MDLs のチェーンでペイロードを指定できます。 これにより、転送バッファーを物理メモリ内に分割できるため、バッファーの数、サイズ、およびアラインメントに関する制限がなくなります。 チェーン MDLs を使用すると、データ転送中のパフォーマンスを向上させることができます。これは、ダブルバッファリングを回避するためです。 詳細については、「チェーン化された[MDL を送信する方法](how-to-send-chained-mdls.md)」を参照してください。

-   複合デバイスの関数の中断とリモートウェイクアップ。

    この機能により、複合デバイスの機能は、他の機能とは無関係に低電力状態に入ることができます。 関数ドライバーは、デバイスによって開始されるリモートウェイクアップを要求することもできます。 このような要求は、複合デバイスの親ドライバーによって処理される必要があります。 Microsoft 提供の親ドライバー (Usbccgp) では、関数の中断機能とリモートウェイクアップ機能がサポートされています。 Windows 8 用の WDK は、置換された親ドライバーがこれらの機能を実装できるようにする DDIs を提供します。 詳細については、「[複合ドライバーで関数の中断を実装する方法](how-to--implement-remote-and-function-wake-support.md)」を参照してください。

## <a name="client-contract-version-for-usb-client-drivers"></a>USB クライアントドライバーのクライアントコントラクトのバージョン


*クライアントコントラクトバージョン*は、USB ドライバースタックに要求を送信するときにクライアントドライバーが持つ一連の規則を識別します。 そうしないと、予期しない動作が発生する可能性があります。 これらのルールの詳細については、「[ベストプラクティス: URBs の使用](usb-client-driver-contract-in-windows-8.md)」を参照してください。

3\.0 デバイスで USB ドライバースタックの機能を使用する予定のクライアントドライバーは、クライアントコントラクトバージョンの USBD\_CLIENT\_CONTRACT\_VERSION\_602 で識別する必要があります。 USB ドライバースタックに登録するには、このようなクライアントドライバーが必要です。 登録後、クライアントドライバーは、基礎となる USB ドライバースタックに対してクエリを実行し、スタックが必要な機能をサポートしているかどうかを判断する必要があります。 これらの操作を容易にするために、次の KMDF 固有のメソッドと WDM ルーチンが、Windows 8 の WDK に含まれています。

| ユースケース                                                           | KMDF ベースのドライバーは...                                                                                                              | WDM ドライバーは...                                                                                          |
|--------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
| クライアントコントラクトのバージョンと USB ドライバースタックを指定するには | [**WdfUsbTargetDeviceCreateWithParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)メソッドを呼び出します。                                      | [**USBD\_CreateHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_createhandle)ルーチンを呼び出します。                                                |
| 特定の機能を照会するには                               | [**WdfUsbTargetDeviceQueryUsbCapability**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability)を呼び出し、クエリを実行する機能の GUID を指定します。 | [**USBD\_QueryUsbCapability ビリティ**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh406230(v=vs.85))を呼び出して、クエリを実行する機能の GUID を指定します。 |

 

## <a name="new-routines-for-allocating-and-building-urbs"></a>URBs を割り当てて構築するための新しいルーチン


Windows 8 には、URBs を割り当て、書式設定、および解放するための新しいルーチンが用意されています。 [**URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)構造体は、USB ドライバースタックによって割り当てられます。 基になるスタックが新しい USB ドライバースタックの場合、URB は不透明な URB コンテキストとペアになります。 USB ドライバースタックは URB コンテキストを使用して、URB の追跡と処理を改善します。 ルーチンの詳細については、「 [URBs の割り当てとビルド](how-to-add-xrb-support-for-client-drivers.md)」を参照してください。

新しいルーチンは次のとおりです。

-   [**USBD\_Ur・検索**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_urballocate)
-   [**USBD\_IsochUrbAllocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_isochurballocate)
-   [**USBD\_SelectConfigUrbAllocateAndBuild**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectconfigurballocateandbuild)
-   [**USBD\_SelectInterfaceUrbAllocateAndBuild**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectinterfaceurballocateandbuild)
-   [**USBD\_UrbFree**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_urbfree)
-   USBD\_は、URB を IRP に関連付けるために[**Urbtoiostacklocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_assignurbtoiostacklocation)ルーチンを割り当てます。 このルーチンは、WDM クライアントドライバーにのみ適用されます。

前の一覧のルーチンに加えて、追加の URB 割り当て用の新しい KMDF 固有のメソッドがあります。 KMDF ベースのクライアントドライバーの場合、を呼び出すことをお勧めします。

-   WdfUsbTargetDeviceCreateUrb メソッド ( [ **\_USBD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_urballocate)ではなく[](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateurb) ) を指定して、URB を割り当てます。
-   ( [**USBD\_IsochUrbAllocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_isochurballocate)ではなく) [**WdfUsbTargetDeviceCreateIsochUrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateisochurb)メソッドを使用して、アイソクロナス転送の URB を割り当てます。 これらの呼び出しでは、転送に必要なアイソクロナスパケットの数に基づいて、可変サイズの URB が割り当てられます。 アイソクロナス転送の詳細については、「[データを USB アイソクロナスエンドポイントに転送する方法](transfer-data-to-isochronous-endpoints.md)」を参照してください。

## <a name="new-user-mode-io-control-requests-for-usb-30-hubs"></a>USB 3.0 ハブの新しいユーザーモード i/o 制御要求


Windows 8 には、アプリケーションが USB 3.0 ハブとそのポートに関する情報を取得するために使用できる新しい Ioctl が用意されています。 新しい Ioctl は次のようになります。

-   [**IOCTL\_USB\_\_ハブ\_情報を取得\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_usb_get_hub_information_ex)
-   [**IOCTL\_USB\_\_ポート\_コネクタの\_プロパティを取得します。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_usb_get_port_connector_properties)
-   [**IOCTL\_USB\_\_ノード\_接続\_情報\_EX\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_usb_get_node_connection_information_ex_v2)

前の i/o 要求を USB ドライバースタックに送信すると、アプリケーションは次の情報を取得します。

-   ハブ記述子
-   すべてのポートとコンパニオンポートのプロパティ
-   ポートに接続されているデバイスの動作速度

## <a name="new-compatible-id-for-winusb"></a>WinUSB 用の新しい互換性 ID


デバイスの製造元は、Windows がデバイスを WinUSB デバイスとして認識できるように、ファームウェア (Microsoft OS 機能記述子) に "WINUSB" を追加できます。 Windows 8 では、Winusb .inf は、デバイス識別子文字列として、USB\\MS\_COMP\_WINUSB を含むように変更されています。 この変更により、デバイスが検出されるとすぐに Winusb .sys がデバイスの関数ドライバーとして自動的に読み込まれるようになります。 詳細については、「 [Winusb デバイス](automatic-installation-of-winusb.md)」を参照してください。

## <a name="new-visual-studio-templates-for-usb-client-drivers-new-for-beta"></a>USB クライアントドライバー用の新しい Visual Studio テンプレート *(ベータ版の\*)*


Microsoft Visual Studio 2012 には、 **Usb ユーザーモードドライバー**と、UMDF および kmdf usb クライアントドライバーのスタートコードを生成する**Usb カーネルモードドライバー**テンプレートが含まれています。 テンプレートコードは、ハードウェアとの通信を可能にするために、USB ターゲットデバイスオブジェクトを初期化します。 詳しくは、次のトピックをご覧ください。

-   [最初の USB クライアントドライバー (UMDF) を作成する方法](implement-driver-entry-for-a-usb-driver--umdf-.md)
-   [最初の USB クライアントドライバー (KMDF) を作成する方法](tutorial--write-your-first-usb-client-driver--kmdf-.md)

詳細については、「 [USB クライアントドライバーの開発の](getting-started-with-usb-client-driver-development.md)概要」を参照してください。 [USB クライアントドライバーの一般的なタスク](wdk-resources-for-usb-driver-development.md)を実行して、ドライバーを拡張します。

UMDF および KMDF ドライバーを実装する方法の詳細については、「 *Windows Driver Foundation を使用*してドライバーを開発する」を参照してください。

## <a name="uasp-driver"></a>UASP ドライバー


Windows 8 には、USB 接続 SCSI プロトコル (UASP) を実装する新しい USB 記憶装置ドライバーが含まれています。 新しいドライバーは、公式の USB 3.0 仕様に従って、一括エンドポイントに静的ストリームを使用します。

## <a name="boot-support"></a>ブートのサポート


Windows to 進む機能を使用すると、Windows がフラッシュドライブまたは外部ドライブから起動できるようになります。 Windows のコピーを、さまざまなコンピューターのドライブから起動できます。

## <a name="enhanced-debugging-and-diagnostic-capabilities"></a>強化されたデバッグ機能と診断機能


Windows 8 には、USB の問題をより迅速に診断するための新しい USB 3.0 デバッグツールが用意されています。 USB 3.0 ホストコントローラーとデバイスの状態を調べる新しい USB 3.0 カーネルデバッガー拡張機能が用意されています。 Usb WPP とイベントトレースを使用して、usb 相互作用を分析し、USB デバイスの問題のトラブルシューティングをより簡単に行うことができます。 Windows 8 は、USB 3.0 でのデバッグをサポートしています。 詳細については、「 [USB 3.0 接続を手動で設定する](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-usb-3-0-debug-cable-connection)」を参照してください。

## <a name="new-usb-specific-failure-messages-in-device-manager"></a>デバイスマネージャーの新しい USB 固有のエラーメッセージ


場合によっては、Windows は接続されている USB デバイスの列挙に失敗することがあります。 通常、列挙エラーは、USB デバイスに送信された要求が失敗した場合、またはデバイスが間違った記述子を返した場合に発生します。

Windows 8 では、このようなエラーが発生すると、**デバイスマネージャー**の **[全般**] タブに、エラーの原因を示す USB 固有のエラーメッセージが表示されます。

エラー文字列は次のとおりです。

-   USB デバイス記述子の要求に失敗しました。
-   USB アドレス設定要求が失敗しました。
-   USB ポートのリセット要求が失敗しました。
-   USB デバイスの以前のインスタンスは削除されませんでした。
-   USB デバイスが無効な USB 構成記述子を返しました。
-   USB デバイスが無効な USB デバイス記述子を返しました。
-   レジストリにアクセスできません。
-   USB 構成記述子の要求が失敗しました。
-   USB デバイスのポートの状態の要求に失敗しました。
-   USB デバイスが無効なシリアル番号文字列を返しました。
-   USB set SEL 要求が失敗しました。
-   USB BOS 記述子の要求が失敗しました。
-   USB デバイスの修飾子記述子の要求に失敗しました。
-   USB シリアル番号の文字列記述子の要求が失敗しました。
-   USB 言語 ID の文字列記述子の要求に失敗しました。
-   USB 製品説明文字列記述子の要求が失敗しました。
-   Microsoft OS 拡張構成記述子の要求に失敗しました。
-   Microsoft OS コンテナー ID 記述子の要求が失敗しました。
-   USB デバイスが無効な USB BOS 記述子を返しました。
-   USB デバイスが無効な USB デバイスの修飾子記述子を返しました。
-   USB デバイスが無効な USB 言語 ID 文字列記述子を返しました。
-   USB デバイスが無効な Microsoft OS コンテナー ID 記述子を返しました。
-   USB デバイスが無効な Microsoft OS 拡張構成記述子を返しました。
-   USB デバイスが無効な製品説明文字列記述子を返しました。
-   USB デバイスが無効なシリアル番号の文字列記述子を返しました。

## <a name="related-topics"></a>関連トピック
[USB ドライバーの新版](https://docs.microsoft.com/windows-hardware/drivers/what-s-new-in-driver-development)  
[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/)  



