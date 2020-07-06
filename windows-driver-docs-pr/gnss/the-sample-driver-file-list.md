---
title: 位置情報サンプルドライバーファイルリスト
description: 位置情報ドライバーのサンプルのソースファイルには、次のカテゴリのファイルが含まれています。
ms.assetid: 8A9A1102-921B-40FF-94F2-FA9E3C1CE662
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73e7f8ccac5fe92c1f0a0d3b5f24ade5c3c2a59c
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968259"
---
# <a name="geolocation-sample-driver-file-list"></a>位置情報サンプルドライバーファイルリスト

> [!IMPORTANT] 
> Windows 8.1 のこのドキュメントと位置情報ドライバーのサンプルは、非推奨とされました。

位置情報ドライバーのサンプルのソースファイルには、次のカテゴリのファイルが含まれています。

-   UMDF センサードライバーに共通の一般的なファイル。
-   シミュレートされた位置情報センサーのサポートを示すために用意されているセンサー固有のファイル。

次の表では、UMDF センサードライバーに共通の一般的なファイルについて説明します。

| ファイル名                          | 内容                                                                                                                                                                                                                   |
|------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| デバイス .cpp                         | CMyDevice メンバー関数の実装が含まれています。 これには、センサークラス拡張を作成して初期化する**onモジュール**が含まれます。                                                     |
| デバイス .h                           | CMyDevice クラスの定義が含まれています。                                                                                                                                                                             |
| Dllsup .cpp                         | ドライバー DLL のエントリポイント (DLLMain) を格納します。                                                                                                                                                                           |
| ドライバー .cpp                         | CMyDriver メンバー関数の実装が含まれています。 これには、CMyDevice クラスのインスタンスを作成する**Ondeviceadd**メソッドが含まれます (「デバイスの説明」を参照してください)。                                    |
| Driver. h                           | CMyDriver クラスの定義が含まれています。                                                                                                                                                                              |
| 内部 .h                         | サンプルドライバーのローカル型定義が含まれています。                                                                                                                                                                     |
| Makefile. inc.                       | をビルドするために必要です。INF ファイル。                                                                                                                                                                                            |
| キュー .cpp                          | CMyQueue メンバー関数の実装が含まれています。 これには、デバイスの i/o キューのインスタンスを作成する**CreateInstance**メソッドが含まれます。                                                       |
| Queue .h                            | CMyQueue クラスの定義が含まれています。                                                                                                                                                                               |
| Resource.h                         | SensorsGeolocationSample. h によって使用される定義が含まれています。                                                                                                                                                               |
| センサー. .cpp                         | CSensor メンバー関数の実装が含まれています。 これには、サポートされるプロパティとデータフィールドのリストを返すメソッドと、書き込み可能なプロパティとデータフィールドを設定するメソッドが含まれます。              |
| センサー. h                           | CSensor クラスの定義が含まれています。                                                                                                                                                                                |
| SensDDI .cpp                        | CSensorDdi クラスの ISensorDriver callback インターフェイスの実装を格納します。 センサークラス拡張は、このインターフェイスのメソッドを呼び出して、オブジェクト、プロパティ、イベントなどのサポートされているデータを取得します。 |
| SensorManager .cpp                  | CSensorManager クラスの実装が含まれています。 このクラスのメソッドは、名前として、センサーデバイスの開始、停止、デバイス状態の取得などを意味します。                        |
| SensorManager. h                    | CSensorManager クラスの定義が含まれています。                                                                                                                                                                       |
| SensorsGeolocationDriverSample .def | モジュールパラメーターを宣言します。                                                                                                                                                                                            |
| SensorsGeolocationDriverSample.htm | サンプルドライバーの概要について説明します。                                                                                                                                                                    |
| SensorsGeolocationDriverSample .idl | ドライバーの COM コンポーネントに必要な定義が含まれています。                                                                                                                                                         |
| SensorsGeolocationDriverSample .inf | X86 および amd64 コンピューターにインボックスドライバーをインストールするときに Windows セットアップ必要な情報が含まれています。                                                                                                        |
| SensorsGeolocationDriverSample .rc  | ファイルの種類、ファイルの説明文字列、ファイルのバージョン、元のファイル名など、ドライバーに必要なリソースの定義が含まれています。                                                                             |
| 変換元                            | ビルドユーティリティによって認識される一連のマクロ定義が含まれています                                                                                                                                            |

 

次の表に、サンプルドライバーでサポートされている、シミュレートされた位置情報センサーをサポートするファイルを示します。

**ファイル名**: 内容

**位置情報 .cpp**: cgeolocation 位置情報クラスの実装が含まれています。 このクラスのメソッドは、シミュレートされたセンサーを初期化し、読み取り可能なプロパティを取得して、書き込み可能なプロパティを設定します。

**位置情報. h**: cgeolocation 位置情報クラスの定義が含まれています


 

## <a name="related-topics"></a>関連トピック
[センサーの地理位置情報ドライバーのサンプル](sensors-geolocation-driver-sample.md)  



