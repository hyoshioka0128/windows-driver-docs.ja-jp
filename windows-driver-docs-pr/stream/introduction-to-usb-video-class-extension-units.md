---
title: USB ビデオ クラス拡張ユニットの概要
description: USB ビデオ クラス拡張ユニットの概要
ms.assetid: a46feb97-771e-4efd-872e-4a4b0fb3b705
keywords:
- 単位の拡張機能の拡張機能ユニット WDK USB ビデオ クラス
- USB ビデオ クラス ドライバー WDK AVStream、拡張機能ユニットについて
- ビデオ ドライバー WDK USB、拡張機能のユニットをクラスについて
- UVC ドライバー WDK AVStream、拡張機能のユニットについて
- 拡張機能ユニット WDK USB ビデオ クラスについて
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9035d8bf3dca7e0b912e52a58b36df65ea12002
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360665"
---
# <a name="introduction-to-usb-video-class-extension-units"></a>USB ビデオ クラス拡張ユニットの概要


*USB ビデオ クラス*仕様には、その仕様に準拠して単位の拡張機能の動作を記述するデバイスの機能を拡張するためのメカニズムが定義されています。 独立系ハードウェア ベンダー (Ihv) は、移動する機能を追加して自分のデバイスの価値を高めることができます、仕様で説明されている以外にもします。

この拡張メカニズムには、アプリケーションは、これらの拡張機能を使用できるようにオペレーティング システムのサポートとユーザー モードのいくつかプラグインが必要があります。 USB ビデオ クラス ドライバーのアーキテクチャは、Ihv は COM Api とデバイスの拡張機能を公開できるように、このようなメカニズムを提供します。 このドキュメントでは、作成し、このようなプラグインの登録に必要な手順について説明します。

### <a name="sdk-information"></a>SDK の情報

IKsTopologyInfo、ISelector および IKsNodeControl は、Vidcap.h で定義されます。

Windows Vista およびそれ以降のリリースでは、Vidcap.h は、Microsoft Windows SDK の一部として含まれています。

Microsoft DirectShow のドキュメントには、対応するリファレンス ページが含まれています。 グローバル一意識別子 (GUID) の型とその他の USB ビデオに関連する定数は、Ksmedia.h で定義されます。 詳細については、次を参照してください。 [USB ビデオ クラス プロパティ](usb-video-class-properties.md)と[カーネル ストリーミング トポロジ ノード](https://docs.microsoft.com/windows-hardware/drivers/stream/kernel-streaming-topology-nodes)します。

 

 




