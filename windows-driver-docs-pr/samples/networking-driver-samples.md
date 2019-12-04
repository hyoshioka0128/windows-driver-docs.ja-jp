---
title: ネットワーク ドライバーのサンプル
description: このディレクトリのドライバーサンプルは、デバイスのカスタムネットワークドライバーを作成するための開始点となります。
ms.assetid: 97C88E82-96AA-41AD-9B1F-3EB848A08BD8
ms.date: 12/02/2019
ms.localizationpriority: medium
ms.openlocfilehash: 8384011200e13b5f3a5c308a04d23b78d7475084
ms.sourcegitcommit: 30fa63ad13fd5e2e883b76a44f0703e01049ffa1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2019
ms.locfileid: "74735256"
---
# <a name="networking-driver-samples"></a>ネットワーク ドライバーのサンプル

このディレクトリのドライバーサンプルは、デバイスのカスタムネットワークドライバーを作成するための開始点となります。

| サンプル | 説明 |
| --- | --- |
| [Bindview](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/bindview-network-configuration-utility) | INetCfg Api を使用してネットワークコンポーネントの列挙、インストール、アンインストール、バインド、およびバインド解除を行う方法を示すアプリケーション。 |
| [Fakemodem](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/fakemodem-driver) | コントローラーレスの単純なモデムドライバーを示します。 |
| [Hyper-v 拡張可能スイッチ拡張機能フィルター](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/hyper-v-extensible-switch-extension-filter-driver) | Hyper-v 拡張可能スイッチ拡張機能フィルタードライバーを実装するために使用される基本ライブラリ。 |
| [NDIS 6.0 フィルター](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/ndis-60-filter-driver) | このサンプルは、NDIS 6.0 フィルタードライバーの基本原則を示す do i のパススルー NDIS 6 フィルタードライバーです。 |
| [NDIS MUX 中間ドライバーと通知オブジェクト](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/ndis-mux-intermediate-driver-and-notify-object) | "N:1" MUX ドライバーの動作を示す NDIS 6.0 ドライバー。 このサンプルでは、1つ下のアダプターの上に複数の仮想ネットワークデバイスを作成します。 |
| [コネクションレス NDIS 6.0 および6.3 プロトコルドライバー](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/ndis-connection-less-protocol-wdm-driver-sample) | このドライバーは、ユーザーモードからの ReadFile 呼び出しや WriteFile 呼び出しを使用して、未加工のイーサネットフレームの送受信をサポートします。 NDIS プロトコルドライバーとして、イーサネットアダプターへのバインドを確立して破棄する方法について説明します。 |
| [コネクションレス NDIS 6.0 プロトコルドライバー](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/connection-less-ndis-60-protocol-kmdf-sample-driver)| このドライバーは、ユーザーモードからの ReadFile 呼び出しや WriteFile 呼び出しを使用して、未加工のイーサネットフレームの送受信をサポートします。 NDIS プロトコルドライバーとして、イーサネットアダプターへのバインドを確立して破棄する方法について説明します。 |
| [NDIS 仮想ミニポートドライバー](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/ndis-virtual-miniport-driver) | 物理ネットワークアダプターを必要としない NDIS ミニポートドライバーの機能を示します。 |
| [OSR USB FX2 Development Board 用のラジオスイッチテストドライバー](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/radio-switch-test-driver-for-osr-usb-fx2-development-board) | OSR USB FX2 Development Board のラジオスイッチ用の HID ドライバーを構成する方法を示します。 |
| [ラジオマネージャー](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/windows-radio-management-sample) | Windows ラジオ管理 Api で使用するためのラジオマネージャーを構成する方法について説明します。 |
| [WDI サンプル](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/wdi-samples) | このサンプルでは、WLAN WDI の使用方法を示します。 |
| [WFP パケットの変更](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/windows-filtering-platform-packet-modification-sample) | Windows Filtering Platform (WFP) のパケット変更機能について説明します。 |
| [WFP トラフィック検査](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/windows-filtering-platform-traffic-inspection-sample) | Windows Filtering Platform (WFP) のトラフィック検査機能について説明します。  |
| [WFP MSN Messenger モニタ](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/windows-filtering-platform-msn-messenger-monitor-sample) | Windows Filtering Platform (WFP) のストリーム検査機能をデモンストレーションするサンプルアプリケーションとドライバー。 |
| [WFP ストリームの編集](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/windows-filtering-platform-stream-edit-sample) | Windows Filtering Platform (WFP) を使用して、伝送制御プロトコル (TCP) 接続の文字列パターンを置き換える方法を示します。 |
| [Windows フィルタリングプラットフォーム](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/windows-filtering-platform-sample) | これは、サンプルのファイアウォールです。 さまざまな条件下でさまざまな WFP レイヤーにフィルターを追加できるコマンドラインインターフェイスを備えています。 また、挿入、基本アクション、プロキシ、およびストリーム検査用のコールアウトも公開されています。 |
| [ネイティブ Wi-fi IHV サービス](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/ihv-sample-ui) | ネイティブ Wi-fi の IHV 拡張機能を示します。 |
| [WSK TCP Echo サーバー](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/wsk-tcp-echo-server) | このサンプルドライバーは、Winsock カーネル (WSK) プログラミングインターフェイスの使用方法を示すために用意されている最小限のドライバーです。 |
