---
title: ドライバーのサンプル ファイルの一覧
description: 次のソース ファイルは、src\SPB\SpbAccelerometer フォルダーにされ、SpbAccelerometer.sys と SpbAccelerometer.inf ファイルの作成に使用されます。
ms.assetid: 48965F7F-1396-4E08-974B-3613684FAA6E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92ecbd4aaadc85fee58e387c3d226e895d067708
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345092"
---
# <a name="the-driver-sample-file-list"></a>ドライバーのサンプル ファイルの一覧


次のソース ファイルは、src\\SPB\\SpbAccelerometer.sys と SpbAccelerometer.inf ファイルをビルドするために使用 SpbAccelerometer フォルダーとは。

|                         |                                                                                                                                                                          |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ファイル                    | 説明                                                                                                                                                              |
| AccelerometerDevice.cpp | センサーを構成するデバイス レベルのメソッドは、プロパティを設定し、データを照会します。                                                                                                |
| Adxl345.h               | デバイスの登録のセットの定義と定義                                                                                                                             |
| ClientManager.cpp       | ドライバーのクライアントが設定可能なプロパティの決定を含む、ロジックの追跡を実装します。                                                                             |
| Device.cpp              | WDF PnP イベントのコールバックとヘルパー メソッド                                                                                                                               |
| DllMain.cpp             | ドライバーのエントリ ポイントと COM サポートを提供するエクスポートされた関数                                                                                                    |
| Driver.cpp              | WDF のドライバー エントリ イベントのコールバックとヘルパー メソッド                                                                                                                      |
| internal.h              | 一般的なにはが含まれています                                                                                                                                                          |
| makefile.inc            | カスタム ビルド アクションを定義します。 変換が含まれています、します。INX ファイルに、します。INF ファイルです。                                                                                 |
| Queue.cpp               | IQueueCallbackDeviceIoControl の実装です。                                                                                                                         |
| ReportManager.cpp       | ドライバーのレポート間隔を保持します。                                                                                                                                  |
| Request.idl             | センサー デバイスと通信するため、要求インターフェイスを定義します。                                                                                                  |
| SensorDdi.cpp           | センサー ドライバーのコールバック インターフェイス、ISensorDriver の実装。                                                                                                   |
| SensorDevice.idl        | DDI センサーおよびセンサー デバイス実装の間のインターフェイスを定義します。                                                                                      |
| ソース                 | リストのソース ファイルとビルド オプション                                                                                                                                     |
| sources.dep             | ビルドの依存関係を定義します。                                                                                                                                               |
| SpbAccelerometer.asl    | 周辺機器のノードのサンプルの ASL ファイルです。 I2C と GPIO 割り込みのリソースを宣言します。 各マクロが直接的な依存関係を記述する ACPI のパスを指定することに注意してください。 |
| SpbAccelerometer.ctl    | ドライバーの宣言のトレース GUID                                                                                                                                     |
| SpbAccelerometer.def    | COM サポートを提供するエクスポートされた関数の宣言                                                                                                              |
| SpbAccelerometer.idl    | ドライバーのライブラリ インターフェイス ファイル                                                                                                                                          |
| SpbAccelerometer.inx    | ドライバーのインストールについて説明します。 ビルド プロセスでは、これに変換します、。 INF します。                                                                                   |
| SpbAccelerometer.rc     | リソース ファイル                                                                                                                                                            |
| SpbRequest.cpp          | デバイスの登録ベースの実装は、SPB を使用してアクセスします。                                                                                                                |
| Trace.h                 | WPP トレースを設定します。                                                                                                                                                     |

 

## <a name="related-topics"></a>関連トピック
[SpbAccelerometer ドライバーのサンプル](spbaccelerometer-driver-sample.md)  



