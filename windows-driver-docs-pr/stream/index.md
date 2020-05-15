---
title: ストリーミング メディア デバイス ドライバー設計ガイド
description: ストリーミング メディア デバイス ドライバー設計ガイド
ms.assetid: 321edd72-4f6a-4eaf-85bf-3b36680a522c
keywords:
- ストリーミング メディア WDK
- メディア ストリーミング WDK
- データ ストリーミング WDK
ms.date: 05/05/2020
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: 1d34676382bc467382271fa9b436a7771377657a
ms.sourcegitcommit: 958a5ced83856df22627c06eb42c9524dd547906
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83235376"
---
# <a name="streaming-media-device-driver-design-guide"></a>ストリーミング メディア デバイス ドライバー設計ガイド

このセクションのガイダンスを使用して、ビデオとオーディオをストリーミングするデバイス (Web カメラ、デジタル カムコーダーなど) 用のドライバーを設計および実装します。

## <a name="in-this-section"></a>このセクションの内容

- [USB ビデオ クラス (UVC) カメラ実装ガイド](uvc-camera-implementation-guide.md)

- [USB ビデオ クラス (UVC) ドライバー実装チェックリスト](uvc-driver-implementation-checklist.md)

- [ネットワーク カメラの設計ガイド](network-camera-design-guide.md)

- [フレーム サーバーのカスタム メディア ソース](frame-server-custom-media-source.md)

- [Windows 10 用の汎用カメラ ドライバー設計ガイド](windows-10-technical-preview-camera-drivers-design-guide.md)

- [共同インストーラーを使用しない USB デバイスのデバイス ファームウェアの更新](device-firmware-update-for-usb-devices-without-using-a-co-installer.md)

- [360 度カメラのビデオ キャプチャ](360-camera-video-capture.md)

- [カメラの組み込み](camera-intrinsics.md)

- [UVC デバイス用の DShow Bridge 実装ガイダンス](dshow-bridge-implementation-guidance-for-usb-video-class-devices.md)

- [ユニバーサル カメラ ドライバーのカメラ クラス INF ファイルの設定](camera-driver-inf-file-class-setting.md)

- [Windows 10 組み込みカメラ アプリの設定に関する OEM ガイダンス](oem-guidance-on-settings-for-the-windows-10-in-box-camera-app.md)

- [ビデオ手ブレ補正のレジストリ設定](oem-guidance-on-registry-keys-for-video-stabilization.md)

- [拡張カメラ コントロール](standardized-extended-controls-.md)

- [カメラ ドライバー構築ガイド](windows-hello-camera-driver-bring-up-guide.md)

- [カメラ デバイスの向き](camera-device-orientation.md)

- [ストリーミング メディアのサンプル](streaming-media-samples.md)

- [AVStream ミニドライバー](avstream-minidrivers-design-guide.md)

- [AVStream のプロパティ セット](avstream-property-sets.md)

- [エンコーダーのプロパティ セット](encoder-property-sets.md)

- [エンコーダー イベント](encoder-events.md)

- [AV/C プロトコル ドライバー関数コード](av-c-protocol-driver-function-codes.md)

- [AV/C ストリーミングのプロトコル ドライバー関数コード](av-c-streaming-protocol-driver-function-codes.md)

- [AV/C ストリーミングの定数](av-c-streaming-constants.md)

- [ビデオ キャプチャ ミニドライバーのプロパティ セット](video-capture-minidriver-property-sets.md)

- [ビデオ キャプチャ ミニドライバーのイベント セット](video-capture-minidriver-event-sets.md)

- [デバイス変換マネージャーのイベント](device-mft-events.md)

- [Windows 2000 カーネル ストリーミング モデル設計ガイド](windows-2000-kernel-streaming-model-design-guide.md)

- [カーネル ストリーミング プロキシ プラグイン](kernel-streaming-proxy-plug-ins-design-guide.md)

- [カーネル ストリーミングのトポロジ ノード](kernel-streaming-topology-nodes.md)

- [カーネル ストリーミングのインターフェイス セット](kernel-streaming-interface-sets.md)

- [カーネル ストリーミングのイベント セット](kernel-streaming-event-sets.md)

- [カーネル ストリーミングのメソッド セット](kernel-streaming-method-sets.md)

- [ストリーム クラス SRB リファレンス](stream-class-srb-reference.md)

- [DVD デコーダー ミニドライバーのプロパティ セット](dvd-decoder-minidriver-property-sets.md)

- [DVD デコーダー ミニドライバーのイベント セット](dvd-decoder-minidriver-event-sets.md)

- [COM インターフェイス](com-interfaces.md)

- [ブロードキャスト ドライバー アーキテクチャのプロパティ、イベント、メソッド セット](broadcast-driver-architecture-property--event--and-method-sets.md)

- [ブロードキャスト ドライバー アーキテクチャの定数](broadcast-driver-architecture-constants.md)

## <a name="related-sections"></a>関連セクション

- [ストリーミング メディア DDI リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_stream)
