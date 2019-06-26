---
title: サンプル カーネルモード ドライバー
description: サンプル カーネルモード ドライバー
ms.assetid: 09d08e07-e991-458f-aedf-018a0dd20af5
keywords:
- カーネル モード ドライバー WDK サンプル
- サンプル ドライバー WDK のカーネル モード
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8e07cfefcf800ca14704e1b13d65e424d525807
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373384"
---
# <a name="sample-kernel-mode-drivers"></a>サンプル カーネルモード ドライバー

WDK は、さまざまなサンプルのカーネル モード ドライバーを提供します。 WDK をインストールした後、`src\general`サブディレクトリには、すべてのカーネル モード ドライバーに適用できるサンプル ドライバーのコードが含まれています。 サンプルは、オンラインも保持されます。 これらのサンプルを以下に示します。

[**DCHU**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/DCHU)

適用、DCHU[設計原則](../develop/getting-started-with-universal-drivers.md)(宣言型、Componentized、アプリのハードウェア サポート [HSA]、およびユニバーサル API 対応)。  実際のユニバーサル ドライバー パッケージのモデルとして使うことができます。

[**PLX9x5x**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/PLX9x5x)

このサンプルでは、Windows Driver Framework を使用してジェネリック PCI デバイス ドライバーを作成する方法を示します。

[**SimpleMediaSource**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/SimpleMediaSource)

このサンプルでは、カメラとしてインストールすることができます、フレームを生成するカスタム メディア ソースとドライバー パッケージを作成する方法を示します。

[**SystemDma/wdm**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/SystemDma/wdm)

このサンプルでは、V3 システム DMA の使用状況を示します。 どのドライバーは、DMA を使用してハードウェアの場所にデータを書き込むの Windows でサポートされているシステム DMA コント ローラーを使用可能性がありますが表示されます。

[**WinHEC 2017 ラボ**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/WinHEC%202017%20Lab)

[**Windows のパフォーマンスの WinHEC 2017/最適化**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/WinHEC%202017/Optimizing%20Windows%20Performance)

[**キャンセル**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/cancel)  

使用方法を示します[キャンセル セーフ IRP キュー](cancel-safe-irp-queues.md)します。

[**エコー**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/echo)

[**イベント**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/event)  

アプリケーションが通知を要求した場合、ハードウェアのイベントのアプリケーションに通知するカーネル モード ドライバーが使用できるテクニックを示します。 1 つの方法を使用して[イベント オブジェクト](event-objects.md)、もう一方が依存して[キュー](queuing-and-dequeuing-irps.md)イベントが発生するまで、通知要求。

[**filehistory**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/filehistory)

FileHistory サンプルは、定期的なバックアップのスケジュールが停止している場合、ファイル履歴サービスを開始するコンソール アプリケーションです。 アプリケーションには、既定のバックアップ ターゲットとして使用する記憶装置のパス名が、コマンド ライン パラメーターとして必要です。

[**IOCTL サンプル**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/ioctl)

ドライバーが I/O 制御コードをサポートする方法について説明します。

[**obcallback**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/obcallback)

ObCallback サンプル ドライバーでは、プロセスの保護のための登録済みのコールバックの使用を示します。 ドライバーは、プロセスの作成時と呼ばれるコントロールのコールバックを登録します。

[**pcidrv**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/pcidrv)

このサンプルでは、PCI デバイス KMDF ドライバーを作成する方法を示します。 Intel 82557/82558 でサンプルの動作は、PCI Ethernet アダプター (10/100) および Intel 互換に基づいています。

[**perfcounters/kcs**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/perfcounters/kcs)

Kcs サンプル ドライバーでは、カーネル モードのパフォーマンスのライブラリの使用を示します。

[**registry/regfltr**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/registry/regfltr)

RegFltr サンプルでは、レジストリのフィルター ドライバーを作成する方法を示します。

[**トースター**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/toaster)  

準拠しているドライバーの一連のサンプル コードを提供、 [Windows Driver Model](windows-driver-model.md) (WDM)。 このサンプルでは、サンプルのインストール ソフトウェアも含まれています。

[**tracedrv**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/tracing/tracedriver)  

使用する方法を示します[WPP ソフトウェア トレース](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing)します。

[**UMDF ドライバーのスケルトン サンプル**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/umdfSkeleton)

このサンプルでは、ユーザー モード ドライバー フレームワークのバージョン 1 を使用して、最小限のドライバーを作成する方法を示します。

[**HID デバイスの firefly KMDF フィルター ドライバー** ](https://github.com/Microsoft/Windows-driver-samples/tree/master/hid/firefly)フィルター ドライバーを記述する方法を示すと共に、このサンプルではリモートの I/O ターゲット インターフェイスを使用してカーネル モードで HID コレクションを開き、設定および取得する IOCTL 要求を送信する方法を示します。機能のレポートだけでなく、アプリケーションが WMI インターフェイスを使用して、フィルター ドライバーにコマンドを送信する方法。

その他のサブディレクトリ、`\src`ディレクトリには、さまざまな種類のハードウェア用のカーネル モード ドライバーのサンプル コードが含まれます。

## <a name="see-also"></a>関連項目

[Microsoft Windows ドライバー サンプル](https://github.com/Microsoft/Windows-driver-samples)github
