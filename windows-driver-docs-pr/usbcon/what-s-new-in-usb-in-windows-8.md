---
Description: このトピックでは、新機能と Windows 8 でのユニバーサル シリアル バス (USB) クライアント ドライバーの機能強化をまとめたものです。
title: Windows 8 の新機能については、usb
ms.date: 05/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 024c009f11414b810de36df4807ea8eda6ed3f92
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356548"
---
# <a name="windows8-whats-new-for-usb"></a>Windows 8:USB の新機能


このトピックでは、新機能と Windows 8 でのユニバーサル シリアル バス (USB) クライアント ドライバーの機能強化をまとめたものです。

-   [USB 3.0 デバイスで新しいドライバー スタック](#new-driver-stack-for-usb-30-devices)
-   [新しいスタックでサポートされる機能](#features-supported-by-the-new-stack)
-   [USB クライアント ドライバーのクライアントのコントラクトのバージョン](#client-contract-version-for-usb-client-drivers)
-   [割り当ておよび翻訳を構築するための新しいルーチン](#new-routines-for-allocating-and-building-urbs)
-   [USB 3.0 ハブで新しいユーザー モードの I/O 制御要求します。](#new-user-mode-io-control-requests-for-usb-30-hubs)
-   [WinUSB の新しい互換性のある ID](#new-compatible-id-for-winusb)
-   [USB クライアント ドライバー用の新しい Visual Studio テンプレート *(\*ベータ版の新規)* ](#new-visual-studio-templates-for-usb-client-drivers-new-for-beta)
-   [UASP ドライバー](#uasp-driver)
-   [ブートのサポート](#boot-support)
-   [強化されたデバッグと診断機能](#enhanced-debugging-and-diagnostic-capabilities)
-   [新しい USB 固有のエラー メッセージでデバイス マネージャー](#new-usb-specific-failure-messages-in-device-manager)

一般的な USB の新機能については、次を参照してください。 [New for USB ドライバー](https://docs.microsoft.com/windows-hardware/drivers/what-s-new-in-driver-development)します。

## <a name="new-driver-stack-for-usb-30-devices"></a>USB 3.0 デバイスで新しいドライバー スタック


Windows 8 では、USB 3.0 デバイスをサポートする新しい USB ドライバー スタックを提供します。 新しいスタックには、USB 3.0 デバイスが xHCI ホスト コント ローラーに関連付けられている場合は、Windows によって読み込まれるドライバーが含まれています。 新しいドライバーがに基づいて[カーネル モード ドライバー フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/what-s-new-in-driver-development)(KMDF) と、USB 3.0 仕様で定義されている機能を実装します。 新しいドライバーは次のとおりです。

-   Usbxhci.sys
-   Ucx01000.sys
-   Usbhub3.sys

新しいドライバー スタックは、以前のバージョンの Windows オペレーティング システムでテストされ、構築された既存のクライアント ドライバーとの互換性を維持します。

USB ドライバー スタックのアーキテクチャ ブロック図と新しいドライバーの簡単な説明を表示するには、次を参照してください。 [USB 3.0 ドライバー スタック アーキテクチャ](usb-3-0-driver-stack-architecture.md)します。

## <a name="features-supported-by-the-new-stack"></a>新しいスタックでサポートされる機能


USB 3.0 デバイスの USB ドライバー スタックは、多くの新機能をサポートします。 いくつかの機能は、クライアント ドライバーによって構成可能です。 これらの機能は次のとおりです。

-   一括エンドポイントの静的なストリーム。

    ストリームは、1 つの一括エンドポイントへの複数のデータ転送を実行することができます、クライアント ドライバーを提供します。 Windows 8 用 Windows Driver Kit (WDK) では、最大 255 一括エンドポイント ストリームするためのクライアント ドライバーを開くことができますを許可する新しいデバイス ドライバー インターフェイス (Ddi) を提供します。 ストリームが開かれた後、クライアント ドライバーと特定のストリームからのデータ転送を実行できます。 詳細については、次を参照してください。 [USB 一括エンドポイントで静的ストリームを開くおよび閉じる方法](how-to-open-streams-in-a-usb-endpoint.md)します。

-   連鎖 MDLs

    クライアント ドライバーでは、連続したバッファーではなく MDLs のチェーンでペイロードを指定できます。 これにより、転送バッファー数、サイズ、およびバッファーの配置に関する制約を削除するため、物理メモリのセグメント化できます。 連鎖 MDLs を使用すると、ダブル バッファリングを回避するのでにデータ転送中にパフォーマンスが向上することができます。 詳細については、次を参照してください。[チェーン MDL の送信方法](how-to-send-chained-mdls.md)します。

-   関数を中断し、複合デバイス用のリモート ウェイク アップします。

    機能は、開始および終了するその他の関数とは無関係に、低電力状態に複合デバイスの機能を使用できます。 関数のドライバーは、デバイスによって開始されたリモート ウェイク アップを要求することもできます。 このような要求は、複合デバイスの親のドライバーによって処理する必要があります。 リモート ウェイク アップ機能および Microsoft から提供された親ドライバー (Usbccgp.sys) のサポート関数を中断します。 WDK for Windows 8 では、これらの機能を実装するためにドライバーを親に置換できる Ddi を提供します。 詳細については、次を参照してください。[複合ドライバーでは実装関数を中断する方法](how-to--implement-remote-and-function-wake-support.md)します。

## <a name="client-contract-version-for-usb-client-drivers"></a>USB クライアント ドライバーのクライアントのコントラクトのバージョン


A*クライアント コントラクト バージョン*USB ドライバー スタックに送信するときに、クライアント ドライバーが要求規則のセットを識別します。 そのためにはエラー、予期しない動作可能性があります。 これらのルールについては、次を参照してください。[ベスト プラクティス。翻訳を使用して](usb-client-driver-contract-in-windows-8.md)します。

USBD のクライアントのコントラクトのバージョンを識別する必要がありますが 3.0 のデバイスの USB ドライバー スタックの機能を使用するクライアント ドライバー\_クライアント\_コントラクト\_バージョン\_602 します。 USB ドライバー スタックを登録するには、このようなクライアント ドライバーが必要です。 クライアント ドライバーは、登録した後、スタックが、必要な機能をサポートするかどうかを確認するのには、基になる USB ドライバー スタックをクエリする必要があります。 これらの操作を容易に KMDF 固有の次のメソッドおよび WDM ルーチンが含まれています for Windows 8 WDK:

| ユース ケース                                                           | KMDF ドライバーにする必要があります.                                                                                                              | WDM ドライバーが必要です。                                                                                          |
|--------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
| クライアントのコントラクト バージョンを指定して、USB ドライバー スタック | 呼び出す、 [ **WdfUsbTargetDeviceCreateWithParameters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)メソッド。                                      | 呼び出す、 [ **USBD\_CreateHandle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_createhandle)ルーチン。                                                |
| 特定の機能を照会するには                               | 呼び出す[ **WdfUsbTargetDeviceQueryUsbCapability** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability)クエリする機能の GUID を指定します。 | 呼び出す[ **USBD\_QueryUsbCapability** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh406230(v=vs.85))クエリする機能の GUID を指定します。 |

 

## <a name="new-routines-for-allocating-and-building-urbs"></a>割り当ておよび翻訳を構築するための新しいルーチン


Windows 8 は、割り当て、書式設定、および翻訳を解放するための新しいルーチンを提供します。 [ **URB** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb)構造体は、USB ドライバー スタックによって割り当てられています。 基になるスタックが新しい USB ドライバー スタックの場合は、URB 不透明 URB コンテキストにペアリングされています。 USB ドライバー スタックでは、URB を追跡および処理を向上させるために、URB コンテキストを使用します。 ルーチンの詳細については、次を参照してください。[割り当てと構成の翻訳](how-to-add-xrb-support-for-client-drivers.md)します。

新しいルーチンは次のとおりです。

-   [**USBD\_UrbAllocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_urballocate)
-   [**USBD\_IsochUrbAllocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_isochurballocate)
-   [**USBD\_SelectConfigUrbAllocateAndBuild**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_selectconfigurballocateandbuild)
-   [**USBD\_SelectInterfaceUrbAllocateAndBuild**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_selectinterfaceurballocateandbuild)
-   [**USBD\_UrbFree**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_urbfree)
-   [**USBD\_AssignUrbToIoStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_assignurbtoiostacklocation)ルーチンに IRP を URB を関連付けます。 このルーチンは、WDM ドライバーがクライアントにのみ適用されます。

上記のルーチン、URB 割り当て KMDF 固有の新しいメソッドがあります。 KMDF ベースのクライアント ドライバーでは、ことをお勧めする次の項目を呼び出し、

-   [ **WdfUsbTargetDeviceCreateUrb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateurb)メソッド (の代わりに[ **USBD\_UrbAllocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_urballocate))、URB を割り当てることです。
-   [ **WdfUsbTargetDeviceCreateIsochUrb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateisochurb)メソッド (の代わりに[ **USBD\_IsochUrbAllocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_isochurballocate)) を URB を割り当てるアイソクロナスを転送します。 これらの呼び出しでは、可変サイズの URB isochronous パケットが転送に必要な数に基づいているを割り当てます。 アイソクロナス転送の詳細については、次を参照してください。 [USB アイソクロナス エンドポイントへのデータの転送方法](transfer-data-to-isochronous-endpoints.md)します。

## <a name="new-user-mode-io-control-requests-for-usb-30-hubs"></a>USB 3.0 ハブで新しいユーザー モードの I/O 制御要求します。


Windows 8 では、USB 3.0 ハブとそのポートに関する情報を取得するアプリケーションが使用できる新しい Ioctl を提供します。 新しい Ioctl は次のとおりです。

-   [**IOCTL\_USB\_取得\_ハブ\_情報\_例**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_usb_get_hub_information_ex)
-   [**IOCTL\_USB\_取得\_ポート\_コネクタ\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_usb_get_port_connector_properties)
-   [**IOCTL\_USB\_取得\_ノード\_接続\_情報\_EX\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_usb_get_node_connection_information_ex_v2)

送信することによって、USB ドライバーには、前の I/O 要求は、アプリケーションの取得を次の一連の情報にスタックします。

-   ハブ記述子
-   すべてのポートとコンパニオン ポートのプロパティ
-   ポートに接続されているデバイスの速度

## <a name="new-compatible-id-for-winusb"></a>WinUSB の新しい互換性のある ID


デバイスの製造元は、その Windows WinUSB デバイスとして、デバイスを認識するため、(Microsoft OS 機能記述子) のファームウェアで"WINUSB"を追加できます。 USB に Windows 8 で Winusb.inf が変更された\\MS\_COMP\_WINUSB デバイス識別子の文字列として。 その変更をデバイスが検出されるとすぐに、デバイスの機能のドライバーとして Winusb.sys を自動的に読み込む Windows を使用できます。 詳細については、次を参照してください。 [WinUSB デバイス](automatic-installation-of-winusb.md)します。

## <a name="new-visual-studio-templates-for-usb-client-drivers-new-for-beta"></a>USB クライアント ドライバー用の新しい Visual Studio テンプレート *(\*ベータ版の新規)*


Microsoft Visual Studio 2012 を含む**USB ユーザー モード ドライバー**と**USB カーネル モード ドライバー**それぞれ UMDF および KMDF の USB クライアント ドライバーのスターター コードを生成するテンプレート。 テンプレート コードでは、ハードウェアとの通信を有効にするには、USB ターゲット デバイス オブジェクトを初期化します。 詳しくは、次のトピックをご覧ください。

-   [最初、USB クライアント ドライバー (UMDF) を記述する方法](implement-driver-entry-for-a-usb-driver--umdf-.md)
-   [最初、USB クライアント ドライバー (KMDF) を記述する方法](tutorial--write-your-first-usb-client-driver--kmdf-.md)

詳細については、次を参照してください。 [USB クライアント ドライバー開発入門](getting-started-with-usb-client-driver-development.md)します。 ドライバーを実行することによって拡張[USB クライアント ドライバーに関する一般的なタスク](wdk-resources-for-usb-driver-development.md)します。

UMDF および KMDF ドライバーを実装する方法については、Microsoft Press の書籍を参照してください。 *、Windows Driver Foundation でのドライバーの開発*します。

## <a name="uasp-driver"></a>UASP ドライバー


Windows 8 には、USB 接続 SCSI プロトコル (UASP) を実装する新しい USB 記憶装置ドライバーが含まれています。 新しいドライバーは、一括エンドポイント、公式の USB 3.0 仕様どおりの静的なストリームを使用します。

## <a name="boot-support"></a>ブートのサポート


Windows to Go 機能は、フラッシュ ドライブまたは外部ドライブからブートする Windows を使用できます。 さまざまなマシンでこれらのドライブから Windows のコピーで起動できます。

## <a name="enhanced-debugging-and-diagnostic-capabilities"></a>強化されたデバッグと診断機能


Windows 8 には、高速の USB 問題の診断を向上させるために、新しい USB 3.0 デバッグ ツールが用意されています。 USB 3.0 ホスト コント ローラーとデバイスの状態を調べる新しい USB 3.0 カーネル デバッガー拡張機能があります。 USB WPP と USB の相互作用を分析し、USB デバイスの問題のトラブルシューティングをより簡単にするトレース イベントを使用することができます。 Windows 8 では、USB 3.0 経由でのデバッグをサポートします。 詳細については、次を参照してください。[設定を、USB 3.0 接続を手動で](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-usb-3-0-debug-cable-connection)します。

## <a name="new-usb-specific-failure-messages-in-device-manager"></a>新しい USB 固有のエラー メッセージでデバイス マネージャー


Windows は接続された USB デバイスを列挙するために失敗します。 通常、USB デバイスに送信された要求が失敗するし、デバイスが正しくない記述子を返します、列挙体のエラーが発生します。

Windows 8 で、このようなエラーが発生したときに、**全般**] タブの [**デバイス マネージャー**失敗の理由を示す USB に固有のエラー メッセージが表示されます。

エラー文字列は次のとおりです。

-   USB デバイスの記述子の要求が失敗しました。
-   USB 設定、アドレスの要求が失敗しました。
-   USB ポートのリセット要求が失敗しました。
-   USB デバイスの以前のインスタンスは削除されませんでした。
-   USB デバイスには、無効な USB 構成記述子が返されます。
-   USB デバイスには、無効な USB デバイス記述子が返されます。
-   レジストリにアクセスできません。
-   USB の構成記述子の要求が失敗しました。
-   USB デバイスのポートの状態の要求が失敗しました。
-   USB デバイスでは、無効なシリアル番号の文字列が返されます。
-   USB 設定、セルフ_サービス要求に失敗しました。
-   USB BOS 記述子の要求が失敗しました。
-   USB デバイスの修飾子の記述子の要求が失敗しました。
-   USB シリアル番号の文字列記述子の要求が失敗しました。
-   USB 言語 ID 文字列記述子の要求が失敗しました。
-   USB 製品説明文字列記述子の要求が失敗しました。
-   Microsoft OS の要求は拡張構成記述子が失敗しました。
-   Microsoft OS コンテナーの ID 記述子の要求が失敗しました。
-   USB デバイスには、無効な USB BOS 記述子が返されます。
-   USB デバイスには、USB デバイスの無効な修飾子記述子が返されます。
-   USB デバイスには、無効な USB 言語 ID 文字列記述子が返されます。
-   USB デバイスには、無効な Microsoft OS コンテナー ID 記述子が返されます。
-   無効な Microsoft OS 構成記述子の拡張 USB デバイスが返されます。
-   USB デバイスには、無効な製品の説明文字列記述子が返されます。
-   USB デバイスには、無効なシリアル番号の文字列記述子が返されます。

## <a name="related-topics"></a>関連トピック
[USB ドライバーの新機能](https://docs.microsoft.com/windows-hardware/drivers/what-s-new-in-driver-development)  
[ユニバーサル シリアル バス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/)  



