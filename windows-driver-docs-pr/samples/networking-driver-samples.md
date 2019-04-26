---
title: ネットワーク ドライバーのサンプル
description: このディレクトリにドライバーのサンプルでは、デバイスのカスタム ネットワーク ドライバーを記述するための開始点を提供します。
ms.assetid: 97C88E82-96AA-41AD-9B1F-3EB848A08BD8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d32596886982c9e1c549b1cf17ca5ffb73ec4a1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345956"
---
# <a name="networking-driver-samples"></a>ネットワーク ドライバーのサンプル


このディレクトリにドライバーのサンプルでは、デバイスのカスタム ネットワーク ドライバーを記述するための開始点を提供します。

## <a name="networking"></a>ネットワーク


| サンプル名                                                | ソリューション                                                                 | 説明                                                                                                                                                                                                                            |
|------------------------------------------------------------|--------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Bindview                                                   | [Bindview](https://go.microsoft.com/fwlink/p/?LinkId=617732)              | INetCfg の Api を使用して、列挙する方法については、アプリケーションで、インストール、アンインストール、バインド、およびネットワーク コンポーネントのバインドを解除します。                                                                                                         |
| Fakemodem                                                  | [fakemodem](https://go.microsoft.com/fwlink/p/?LinkId=617733)             | 単純なコント ローラーのないモデムのドライバーを示します。                                                                                                                                                                                    |
| HYPER-V 拡張可能スイッチ拡張機能フィルター                 | [extensions](https://go.microsoft.com/fwlink/p/?LinkId=617913)            | HYPER-V 拡張可能スイッチの拡張機能フィルター ドライバーを実装するために使用される基本ライブラリ。                                                                                                                                                  |
| NDIS 6.0 のフィルター処理                                            | [フィルター (filter)](https://go.microsoft.com/fwlink/p/?LinkId=617915)                | このサンプルは、NDIS 6.0 のフィルター ドライバーの基本原則のデモの何もしないパススルー 6 の NDIS フィルター ドライバーです。                                                                                                          |
| MUX の NDIS 中間ドライバとオブジェクトへの通知             | [mux](https://go.microsoft.com/fwlink/p/?LinkId=617916)                   | NDIS 6.0 ドライバーであり、"N:1"MUX ドライバーの操作。 このサンプルでは、アダプターが 1 つ下の上に複数の仮想ネットワーク デバイスを作成します。                                                                        |
| コネクションレス NDIS 6.0 および 6.3 プロトコル ドライバー            | [ndisprot60](https://go.microsoft.com/fwlink/p/?LinkId=617917)            | このドライバーは、ユーザー モードから ReadFile/WriteFile 呼び出しを使用して、生のイーサネット フレームの送受信をサポートします。 NDIS プロトコル ドライバーでは、としては、構築し、破棄のイーサネット アダプターにバインドする方法を示しています。                 |
| コネクションレス NDIS 6.0 プロトコル ドライバー                    | [ndisprot\_kmdf](https://go.microsoft.com/fwlink/p/?LinkId=620197)        | このドライバーは、ユーザー モードから ReadFile/WriteFile 呼び出しを使用して、生のイーサネット フレームの送受信をサポートします。 NDIS プロトコル ドライバーでは、としては、構築し、破棄のイーサネット アダプターにバインドする方法を示しています。                 |
| NDIS 仮想ミニポート ドライバー                               | [netvmini](https://go.microsoft.com/fwlink/p/?LinkId=617918)              | 物理ネットワーク アダプターを必要とせず、NDIS ミニポート ドライバーの機能を示します。                                                                                                                                |
| OSR usb-fx2 の開発ボードのラジオ スイッチ テスト ドライバー | [HidSwitchDriverSample](https://go.microsoft.com/fwlink/p/?LinkId=617919) | OSR usb-fx2 の開発ボードのオプションのスイッチの HID ドライバーを構成する方法を示します。                                                                                                                                   |
| ラジオ マネージャー                                              | [RadioManagerSample](https://go.microsoft.com/fwlink/p/?LinkId=617920)    | Windows ラジオの管理 Api を使用するためラジオ Manager を構成する方法を示します。                                                                                                                                          |
| WFP パケットの変更                                    | [ddproxy](https://go.microsoft.com/fwlink/p/?LinkId=617930)               | Windows フィルタ リング プラットフォーム (WFP) のパケットの変更機能を示します。                                                                                                                                             |
| WFP トラフィックの検査                                     | [検査](https://go.microsoft.com/fwlink/p/?LinkId=617931)               | Windows フィルタ リング プラットフォーム (WFP) のトラフィック検査機能を示します。                                                                                                                                              |
| WFP MSN Messenger Monitor                                  | [msnmntr](https://go.microsoft.com/fwlink/p/?LinkId=617932)               | サンプル アプリケーションとドライバーが Windows フィルタ リング プラットフォーム (WFP) のストリーム検査機能を紹介します。                                                                                                              |
| WFP Stream の編集                                            | [stmedit](https://go.microsoft.com/fwlink/p/?LinkId=617933)               | Windows フィルタ リング プラットフォーム (WFP) を使用する伝送制御プロトコル (TCP) 接続の文字列パターンを置き換えるかを示します。                                                                                               |
| Windows フィルタリング プラットフォーム                                 | [WFPSampler](https://go.microsoft.com/fwlink/p/?LinkId=620198)            | これは、サンプル ファイアウォールです。 さまざまな条件下でさまざまな WFP レイヤーのフィルターを追加できるようにするコマンド ライン インターフェイスがあります。 さらに、挿入、基本的な操作、プロキシ、およびストリームの検査のコールアウトが公開されます。 |
| ネイティブ Wi-fi IHV サービス                                   | [wlan](https://go.microsoft.com/fwlink/p/?LinkId=617934)                  | ネイティブ wi-fi IHV 機能拡張を示します。                                                                                                                                                                                       |
| WSK TCP エコー サーバー                                        | [echosrv](https://go.microsoft.com/fwlink/p/?LinkId=617935)               | このサンプル ドライバーは、Winsock カーネル (WSK) プログラミング インターフェイスの使用法を示すもので最小限のドライバーです。                                                                                                               |

 

 

 




