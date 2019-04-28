---
title: USB ビデオ クラス (UVC) ドライバー実装チェックリスト
description: デバイスの USB ビデオ クラス (UVC) ドライバーを実装する手順について説明します。
ms.date: 01/30/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9ae4a63cf21c92ba4dad28a357fdcf35bbea51d7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367462"
---
# <a name="usb-video-class-uvc-driver-implementation-checklist"></a>USB ビデオ クラス (UVC) ドライバー実装チェックリスト

## <a name="step-1-get-started-with-usb-video-class-uvc-using-documentation-from-usborg-and-microsoft"></a>手順 1:USB ビデオ クラス (UVC) が USB.org とマイクロソフトのドキュメントの使用を開始します。

UVC に慣れ親しむには、これらのリンクを使用します。

- アクセス、 [USB クラス](http://www.usb.org/developers/docs/devclass_docs/)USB.org ドキュメント (非 UVC 固有)

- ダウンロード、 [USB ビデオ クラス 1.5](https://go.microsoft.com/fwlink/p/?linkid=2085170) USB.org からドキュメント

- レビュー、 [USB ビデオ クラス ドライバーの概要](https://docs.microsoft.com/windows-hardware/drivers/stream/usb-video-class-driver-overview)トピック

## <a name="step-2-implement-the-platform-supplied-device-mft"></a>手順 2:デバイスのプラットフォームによって提供される MFT を実装します。

- デバイスのプラットフォームによって提供される MFT は RGB USB カメラ用です。 一般的な機能を提供、たとえば、顔検出ベースの ROI 3A の優先順位付け (カメラのファームウェアには、UVC 1.5 標準で指定された ROI コントロールがサポートされている) 場合。

- この機能を有効にするには、カメラが ROI をサポートしていることを確認する必要があります。 この機能を無効にする必要がある場合 (たとえば、INF ファイル エントリ) のレジストリ キーをこれを行う必要があります。

## <a name="step-3-implement-the-custom-device-mft-and-mft0-for-your-device"></a>手順 3:デバイスのカスタムのデバイス MFT および MFT0 を実装します。

- デバイス MFT は、UVC のユーザー モード コンポーネントです。 拡張機能との差別化要因、UVC を追加するには、このコンポーネントを挿入することができます。

- レビュー、[デバイス MFT 設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/stream/dmft-design)します。

- レビュー、[デバイス MFT サンプル コード](https://github.com/Microsoft/Windows-driver-samples/tree/master/avstream/sampledevicemft)GitHub 上にあります。

- MFT0 で関連情報を確認、 [UWP アプリのデバイスのカメラ driver MFT 作成](https://docs.microsoft.com/windows-hardware/drivers/devapps/creating-a-camera-driver-mft)トピック。

**注**デバイス MFT モデル MFT0 モデルよりも優先されます。 MFT0 モデルをサポートするために Windows が引き続き発生するときに、設計を簡略化し、機能性とスケーラビリティをサポートしているデバイス MFT を代わりに、使用することお勧めします。

## <a name="step-4-implement-microsoft-specified-uvc-extensions"></a>手順 4:Microsoft が指定した UVC 拡張機能を実装します。

- [USB ビデオ クラス 1.5 仕様に対する Microsoft の拡張機能](https://docs.microsoft.com/windows-hardware/drivers/stream/uvc-extensions-1-5)

- [UVC で赤外線のストリームのサポート](https://docs.microsoft.com/windows-hardware/drivers/stream/infrared-stream-support-in-uvc)

- 方法 2 では、キャプチャ静止画像します。

    - USB.org ドキュメント:

        - セクションを復習*メソッド 2*の 17 ページ上で始まる、 *UVC 1.5 クラス specification.pdf*上記の手順 1. でダウンロードしました。

    - Microsoft 固有のドキュメント:

        - 2.2.1 と 2.2.2 でセクションを確認して、 [USB ビデオ クラス 1.5 の仕様に対する Microsoft 拡張機能](https://docs.microsoft.com/windows-hardware/drivers/stream/uvc-extensions-1-5)します。

## <a name="step-5-test-your-uvc-implementation-to-ensure-it-passes-hlk-tests-and-meets-required-functionality-and-performance"></a>手順 5:HLK テストに合格し、必要な機能とパフォーマンスを満たしていることを確認する UVC 実装をテストします。

- 実行[Windows HLK テスト](https://msdn.microsoft.com/library/windows/hardware/dn930814)

- カメラに固有の実行[Device.Streaming HLK テスト](https://msdn.microsoft.com/library/windows/hardware/dn941930)

- カメラの要件を満たしているし、カメラが (たとえば、Skype、Windows こんにちは、およびなど) に準拠してもする必要がありますが、その他の製品 HLK テストが合格を確認してください。
