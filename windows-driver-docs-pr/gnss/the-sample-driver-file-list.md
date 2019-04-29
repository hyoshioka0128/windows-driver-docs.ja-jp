---
title: 地理的位置情報サンプル ドライバー ファイルの一覧
description: 地理的位置情報ドライバー サンプルのソース ファイルには、ファイルの次のカテゴリが含まれています。
ms.assetid: 8A9A1102-921B-40FF-94F2-FA9E3C1CE662
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ab4fbd174231d4a40c8bf3dcfed7525521165b9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63326172"
---
# <a name="geolocation-sample-driver-file-list"></a>地理的位置情報サンプル ドライバー ファイルの一覧

> [!IMPORTANT] 
> このドキュメントと Windows 8.1 の地理的位置情報ドライバー サンプルが非推奨とされました。

地理的位置情報ドライバー サンプルのソース ファイルには、ファイルの次のカテゴリが含まれています。

-   UMDF センサー ドライバーに共通する一般的なファイル。
-   示すために用意されているセンサーに固有のファイルは、シミュレートされた地理的位置情報センサーのサポートします。

次の表では、UMDF センサー ドライバーに共通する一般的なファイルについて説明します。

| ファイル名                          | 目次                                                                                                                                                                                                                   |
|------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Device.cpp                         | CMyDevice のメンバー関数の実装が含まれています。 これが含まれています、 **OnPrepareHardware**メソッドを作成して、センサー クラスの拡張を初期化します。                                                     |
| Device.h                           | CMyDevice クラスの定義が含まれています。                                                                                                                                                                             |
| Dllsup.cpp                         | ドライバー DLL のエントリ ポイント (DLLMain) が含まれています。                                                                                                                                                                           |
| Driver.cpp                         | CMyDriver のメンバー関数の実装が含まれています。 これが含まれています、 **OnDeviceAdd** CMyDevice クラスのインスタンスを作成する方法 (Device.cpp の説明を参照してください)。                                    |
| Driver.h                           | CMyDriver クラスの定義が含まれています。                                                                                                                                                                              |
| internal.h                         | ドライバーのサンプルのローカルの種類の定義が含まれています。                                                                                                                                                                     |
| Makefile.inc                       | ビルドに必要なします。INF ファイルです。                                                                                                                                                                                            |
| Queue.cpp                          | CMyQueue のメンバー関数の実装が含まれています。 これが含まれています、 **CreateInstance**メソッドで、デバイスの I/O キューのインスタンスを作成します。                                                       |
| Queue.h                            | CMyQueue クラスの定義が含まれています。                                                                                                                                                                               |
| Resource.h                         | SensorsGeolocationSample.h によって使用される定義が含まれています。                                                                                                                                                               |
| Sensor.cpp                         | CSensor のメンバー関数の実装が含まれています。 これには、サポートされるプロパティとデータ フィールドの一覧を返すメソッドとプロパティとデータの書き込み可能なフィールドを設定するメソッドが含まれます。              |
| Sensor.h                           | CSensor クラスの定義が含まれています。                                                                                                                                                                                |
| SensDDI.cpp                        | CSensorDdi クラスで ISensorDriver コールバック インターフェイスの実装が含まれています。 センサー クラスの拡張機能は、オブジェクト、プロパティ、およびイベントなどのサポートされているデータを取得するには、このインターフェイスでメソッドを呼び出します。 |
| SensorManager.cpp                  | CSensorManager クラスの実装が含まれています。 このクラスのメソッドの名前が示すように、管理センサー デバイス: し、開始、停止、デバイスの状態を取得します。                        |
| SensorManager.h                    | CSensorManager クラスの定義が含まれています。                                                                                                                                                                       |
| SensorsGeolocationDriverSample.def | モジュールのパラメーターを宣言します。                                                                                                                                                                                            |
| SensorsGeolocationDriverSample.htm | ドライバーのサンプルの概要を説明が含まれています。                                                                                                                                                                    |
| SensorsGeolocationDriverSample.idl | ドライバーの COM コンポーネントのために必要な定義が含まれています。                                                                                                                                                         |
| SensorsGeolocationDriverSample.inf | X86 および amd64 コンピューター インボックス ドライバーをインストールするときに Windows セットアップが必要な情報が含まれています。                                                                                                        |
| SensorsGeolocationDriverSample.rc  | ファイルの種類、ファイルを説明する文字列、ファイルのバージョン、および元のファイル名などのドライバーが必要なリソースの定義が含まれています。                                                                             |
| Sources                            | 一連ビルド ユーティリティで認識されるマクロ定義にはが含まれています                                                                                                                                            |

 

次の表は、サンプル ドライバーでサポートされているシミュレートされた地理的位置情報センサーをサポートするファイルを一覧表示します。

|                 |                                                                                                                                                                             |
|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ファイル名       | 目次                                                                                                                                                                    |
| Geolocation.cpp | CGeolocation クラスの実装が含まれています。 このクラスのメソッドは、シミュレートされたセンサーの初期化、読み取り可能なプロパティを取得し、書き込み可能なプロパティを設定します。 |
| Geolocation.h   | CGeolocation クラスの定義が含まれています                                                                                                                           |

 

## <a name="related-topics"></a>関連トピック
[センサー地理位置情報ドライバー サンプル](sensors-geolocation-driver-sample.md)  



