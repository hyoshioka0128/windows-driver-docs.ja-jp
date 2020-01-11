---
title: USB ビデオ クラス (UVC) ドライバー実装チェックリスト
description: デバイス用の USB ビデオクラス (UVC) ドライバーを実装する手順について説明します。
ms.date: 01/30/2018
ms.localizationpriority: medium
ms.openlocfilehash: 94839ce6a93ffd5b55ea6dde8ff0885210373222
ms.sourcegitcommit: eb1f58d23da3b1240385c072837d9118239a8f97
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2020
ms.locfileid: "75883889"
---
# <a name="usb-video-class-uvc-driver-implementation-checklist"></a>USB ビデオ クラス (UVC) ドライバー実装チェックリスト

## <a name="step-1-get-started-with-usb-video-class-uvc-using-documentation-from-usborg-and-microsoft"></a>手順 1: USB.org と Microsoft のドキュメントを使用して USB ビデオクラス (UVC) の使用を開始する

次のリンクを使用して、UVC について理解します。

- USB.org で[USB クラス](https://www.usb.org/documents?search=&type%5B0%5D=55&items_per_page=50)のドキュメント (uvc 以外) にアクセスする

- [USB ビデオクラス 1.5](https://go.microsoft.com/fwlink/p/?linkid=2085170)のドキュメントを USB.org からダウンロードします。

- [USB ビデオクラスドライバーの概要](https://docs.microsoft.com/windows-hardware/drivers/stream/usb-video-class-driver-overview)に関するトピックを確認します。

## <a name="step-2-implement-the-platform-supplied-device-mft"></a>手順 2: プラットフォームによって提供されるデバイスの MFT を実装する

- プラットフォームによって提供されるデバイス MFT は、RGB USB カメラ用です。 これには一般的な機能が用意されています。たとえば、3A の優先順位付けの顔検出ベースの ROI (カメラのファームウェアが UVC 1.5 標準で指定された ROI 制御をサポートしている場合) です。

- この機能を有効にするには、カメラが ROI をサポートしていることを確認する必要があります。 この機能を無効にする必要がある場合は、レジストリキー (INF ファイルエントリなど) を使用して設定する必要があります。

## <a name="step-3-implement-the-custom-device-mft-and-mft0-for-your-device"></a>手順 3: デバイスのカスタムデバイス MFT と MFT0 を実装する

- デバイス MFT は、UVC のユーザーモードコンポーネントです。 このコンポーネントを挿入して、拡張機能と差別化要因を UVC に追加することができます。

- [DEVICE MFT 設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/stream/dmft-design)を確認します。

- デバイスの[MFT サンプルコード](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/driver-device-transform-sample/)を確認します。

- MFT0 の関連情報については、「 [UWP デバイスアプリ用にカメラドライバー MFT を作成](https://docs.microsoft.com/windows-hardware/drivers/devapps/creating-a-camera-driver-mft)する」を参照してください。

> [!NOTE]
> デバイスの MFT モデルは、MFT0 モデルよりも優先されます。 Windows では MFT0 モデルを引き続きサポートしていますが、設計が簡素化され、より多くの機能とスケーラビリティがサポートされるため、代わりにデバイス MFT を使用することをお勧めします。

## <a name="step-4-implement-microsoft-specified-uvc-extensions"></a>手順 4: Microsoft によって指定された UVC 拡張機能を実装する

- [USB ビデオ クラス 1.5 仕様に対する Microsoft の拡張機能](https://docs.microsoft.com/windows-hardware/drivers/stream/uvc-extensions-1-5)

- [UVC での赤外線ストリームのサポート](https://docs.microsoft.com/windows-hardware/drivers/stream/infrared-stream-support-in-uvc)

- 方法 2: イメージのキャプチャ:

  - USB.org のドキュメント:

    - 前の手順 1. でダウンロードした*Uvc 1.5 クラス仕様*のページ17で開始する*メソッド 2*のセクションを確認します。

  - Microsoft 固有のドキュメント:

    - 「 [Microsoft extensions FOR USB Video Class 1.5 仕様](https://docs.microsoft.com/windows-hardware/drivers/stream/uvc-extensions-1-5)」のセクション2.2.1 と2.2.2 を確認します。

## <a name="step-5-test-your-uvc-implementation-to-ensure-it-passes-hlk-tests-and-meets-required-functionality-and-performance"></a>手順 5: UVC 実装をテストして HLK テストに合格し、必要な機能とパフォーマンスを満たしていることを確認する

- [WINDOWS HLK テスト](https://docs.microsoft.com/windows-hardware/drivers/)の実行

- カメラ固有の[デバイスを実行します。 STREAMING HLK テスト](https://docs.microsoft.com/windows-hardware/test/hlk/testref/device-streaming)

- カメラが要件を満たしていることを確認し、カメラが準拠している必要がある他の製品 (たとえば、Skype、Windows Hello など) に対して HLK テストを渡します。
