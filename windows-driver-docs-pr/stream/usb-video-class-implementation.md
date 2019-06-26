---
title: USB ビデオ クラスの実装
description: USB ビデオ クラスの実装
ms.assetid: b390d741-9ddc-4bac-bca2-73e32461c5ed
keywords:
- USB ビデオ クラス ドライバー WDK AVStream、実装します。
- ビデオのクラス ドライバー WDK USB、実装します。
- UVC ドライバー WDK AVStream、実装します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ff01a736deeb7459cec5a2527539e06835b7a17
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383139"
---
# <a name="usb-video-class-implementation"></a>USB ビデオ クラスの実装


Microsoft 提供の USB ビデオ クラス ドライバー (usbvideo.sys) では、暗証番号 (pin) を中心とした AVStream ミニドライバーです。 各 USB ビデオ クラス フィルター ファクトリを作成しますか? オペレーティング システムによって列挙された準拠しているデバイス インスタンス。 ドライバーでデバイスで、各入力または出力ターミナルの暗証番号 (pin) ファクトリを作成することも、**データフロー**のメンバー、 [ **KSPIN\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kspin_descriptor)構造体関連する値に設定します。

USB ビデオ クラス ドライバーでは、デバイス記述子によって報告されたデバイスの内部のトポロジを使用して、フィルター、ノード、および接続の構成 (KS) トポロジ グラフをストリーミングするカーネルを構築します。

デバイスでサポートされているコントロールの種類と数に基づいて、USB ビデオ クラスに動的にフィルター、暗証番号 (pin)、およびレポート AVStream のフィルターと暗証番号 (pin) の記述子で KS automation テーブル ノードのプロパティ セット。

各ビデオや静止イメージ データ、デバイス エンドポイントでサポートされるデータ形式に基づいて、USB ビデオ クラスは、KS データ範囲がサポートされているとデータの積集合ハンドラーそれぞれ AVStream 暗証番号 (pin) の記述子での対応する一覧を報告します。 USB ビデオ クラス ドライバーを通じて情報をエクスポートする、[カーネル ストリーミング プロキシ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_stream/index)モジュール。

USB ビデオ クラス ドライバーは、オーディオ/ビデオ ストリームの同期化もサポートしています。usbvideo.sys は、KS マスター クロックとして機能し、ビデオのサンプルにタイムスタンプを追加できます。 USB ビデオ クラス仕様には、ハードウェアが、クラス ドライバーをタイミング情報を提供する方法の詳細が含まれています。

USB ビデオ クラスを通信するには、ユーザー モードのクライアントは、DirectShow またはメディア ファンデーションのインターフェイスを呼び出します。 これらのインターフェイスは、プラグインとしてカーネル ストリーミング プロキシによって定義されている COM インターフェイスのラッパーです。に関する詳細については、Microsoft Windows SDK ドキュメントを参照してください[メディア ファンデーション](https://go.microsoft.com/fwlink/p/?linkid=144771)します。

 

 




