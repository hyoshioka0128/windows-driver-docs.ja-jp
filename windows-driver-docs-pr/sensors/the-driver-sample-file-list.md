---
title: ドライバーサンプルファイルの一覧
description: 次のソースファイルは src\SPB\SpbAccelerometer フォルダーにあり、SpbAccelerometer.sys と SpbAccelerometer ファイルをビルドするために使用されます。
ms.assetid: 48965F7F-1396-4E08-974B-3613684FAA6E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c10a577beadf679909079e9d1a61e614b0cc6557
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968111"
---
# <a name="the-driver-sample-file-list"></a>ドライバーサンプルファイルの一覧


次のソースファイルは、src \\ SPB SpbAccelerometer フォルダーにあり、 \\ SpbAccelerometer.sys と SpbAccelerometer ファイルをビルドするために使用されます。

**ファイル**: 説明

**AccelerometerDevice**: センサーの構成、プロパティの設定、データのクエリを行うためのデバイスレベルのメソッド。

**Adxl345**: デバイスのレジスタセットの定義と定義

**Clientmanager .cpp**: 設定可能なプロパティの判別など、ドライバーのクライアント追跡ロジックを実装します。

**デバイス .cpp**: WDF PnP イベントのコールバックとヘルパーメソッド

**DllMain**: ドライバーのエントリポイントと、COM サポートを提供するためのエクスポートされた関数

**ドライバー .cpp**: WDF ドライバーエントリのイベントコールバックとヘルパーメソッド

**内部 .h**: 共通インクルード

**makefile. inc.**: カスタムビルドアクションを定義します。 の変換が含まれます。INX ファイルをに変換します。INF ファイル。

**Queue .cpp**: IQueueCallbackDeviceIoControl の実装。

**Reportmanager .cpp**: ドライバーのレポート間隔を保持します。

**要求 .idl**: センサーデバイスと通信するための要求インターフェイスを定義します。

**Sensorddi .cpp**: センサードライバーのコールバックインターフェイス ISensorDriver の実装。

**Sensordevice .idl**: センサー DDI とセンサーデバイスの実装の間のインターフェイスを定義します。

**ソース**: ソースファイルとビルドオプションを一覧表示します

**ソース. dep**: ビルドの依存関係を定義します

**SpbAccelerometer: asl**: 周辺機器ノードのサンプル asl ファイル。 これは、I2C および GPIO interrupt リソースを宣言します。 各マクロは、直接の依存関係を記述するための ACPI パスを指定することに注意してください。

**SpbAccelerometer**: ドライバーのトレース GUID の宣言

**SpbAccelerometer**: COM サポートを提供するためにエクスポートされた関数の宣言

**SpbAccelerometer**: ドライバーのライブラリインターフェイスファイル

**SpbAccelerometer inx**: ドライバーのインストールについて説明します。 ビルドプロセスでは、これを .INF に変換します。

**SpbAccelerometer**: リソースファイル

**Spbrequest .cpp**: SPB を介した登録ベースのデバイスアクセスの実装。

**Trace .h**: WPP トレースを設定します。


 

## <a name="related-topics"></a>関連トピック
[SpbAccelerometer ドライバーのサンプル](spbaccelerometer-driver-sample.md)  



