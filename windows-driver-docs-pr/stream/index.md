---
title: ストリーミング メディア デバイス ドライバー設計ガイド
description: ストリーミング メディア デバイス ドライバー設計ガイド
ms.assetid: 321edd72-4f6a-4eaf-85bf-3b36680a522c
keywords:
- ストリーミング メディア WDK
- メディア ストリーミング WDK
- データ ストリーミング WDK
ms.date: 11/15/2018
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: a24e49a529644b3f3f51e5339a6788caa48b7bf8
ms.sourcegitcommit: 988d100e4d3b218a59fdac034d39a1816d145c85
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2020
ms.locfileid: "72845577"
---
# <a name="streaming-media-device-driver-design-guide"></a>ストリーミング メディア デバイス ドライバー設計ガイド

このセクションのガイダンスを使用して、ビデオとオーディオをストリーミングするデバイス (Web カメラ、デジタル カムコーダーなど) 用のドライバーを設計および実装します。

## <a name="in-this-section"></a>このセクションの内容

- [共同インストーラーを使用しない USB デバイスのデバイス ファームウェアの更新](device-firmware-update-for-usb-devices-without-using-a-co-installer.md)
- [USB ビデオ クラス (UVC) カメラ実装ガイド](uvc-camera-implementation-guide.md)
- [フレーム サーバーのカスタム メディア ソース](frame-server-custom-media-source.md)
- [360 カメラのビデオ キャプチャ](360-camera-video-capture.md) (Windows 10 バージョン 1803 向けの新規)
- [カメラの組み込み](camera-intrinsics.md)
- [UVC デバイス用の DShow Bridge 実装ガイダンス](dshow-bridge-implementation-guidance-for-usb-video-class-devices.md)
- [ユニバーサル カメラ ドライバーのカメラ クラス INF ファイルの設定](camera-driver-inf-file-class-setting.md) (Windows 10 バージョン 1709 向けの新規)
- [USB ビデオ クラス (UVC) ドライバー実装チェックリスト](uvc-driver-implementation-checklist.md) (Windows 10 バージョン 1703 向けの新規)
- [カメラ デバイスの向き](camera-device-orientation.md)
- [AVStream ミニドライバー](avstream-minidrivers-design-guide.md)
- [Windows 2000 カーネル ストリーミング モデル設計ガイド](windows-2000-kernel-streaming-model-design-guide.md)
- [カーネル ストリーミング プロキシ プラグイン](kernel-streaming-proxy-plug-ins-design-guide.md)
- [ストリーミング メディアのサンプル](streaming-media-samples.md)
- [Windows 10 組み込みカメラ アプリの設定に関する OEM ガイダンス](oem-guidance-on-settings-for-the-windows-10-in-box-camera-app.md)
- [ビデオ手ブレ補正のレジストリ設定](oem-guidance-on-registry-keys-for-video-stabilization.md)
- [拡張カメラ コントロール](standardized-extended-controls-.md) (Windows 10 バージョン 1607 向けに更新)
- [カメラ ドライバー構築ガイド](windows-hello-camera-driver-bring-up-guide.md) (Windows 10 バージョン 1607 向けの新規)
- [Windows 10 用の汎用カメラ ドライバー設計ガイド](windows-10-technical-preview-camera-drivers-design-guide.md)
- [AVStream のプロパティ セット](avstream-property-sets.md)
- [ブロードキャスト ドライバー アーキテクチャのプロパティ、イベント、メソッド セット](broadcast-driver-architecture-property--event--and-method-sets.md)
- [ブロードキャスト ドライバー アーキテクチャの定数](broadcast-driver-architecture-constants.md)
- [エンコーダーのプロパティ セット](encoder-property-sets.md)
- [エンコーダー イベント](encoder-events.md)
- [AV/C プロトコル ドライバー関数コード](av-c-protocol-driver-function-codes.md)
- [AV/C ストリーミングのプロトコル ドライバー関数コード](av-c-streaming-protocol-driver-function-codes.md)
- [AV/C ストリーミングの定数](av-c-streaming-constants.md)
- [ビデオ キャプチャ ミニドライバーのプロパティ セット](video-capture-minidriver-property-sets.md)
- [ビデオ キャプチャ ミニドライバーのイベント セット](video-capture-minidriver-event-sets.md)
- [デバイス変換マネージャーのイベント](device-mft-events.md)
- [カーネル ストリーミングのトポロジ ノード](kernel-streaming-topology-nodes.md)
- [カーネル ストリーミングのインターフェイス セット](kernel-streaming-interface-sets.md)
- [カーネル ストリーミングのイベント セット](kernel-streaming-event-sets.md)
- [カーネル ストリーミングのメソッド セット](kernel-streaming-method-sets.md)
- [ストリーム クラス SRB リファレンス](stream-class-srb-reference.md)
- [DVD デコーダー ミニドライバーのプロパティ セット](dvd-decoder-minidriver-property-sets.md)
- [DVD デコーダー ミニドライバーのイベント セット](dvd-decoder-minidriver-event-sets.md)
- [COM インターフェイス](com-interfaces.md)

## <a name="related-sections"></a>関連セクション

- [ストリーミング メディア DDI リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_stream)
