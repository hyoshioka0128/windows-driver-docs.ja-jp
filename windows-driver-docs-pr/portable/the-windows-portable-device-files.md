---
Description: Windows ポータブル デバイスのファイル
title: Windows ポータブル デバイスのファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e945f75f97077f340de15e922b2c29c896e70296
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378622"
---
# <a name="the-windows-portable-devices-files"></a>Windows ポータブル デバイスのファイル


WpdHelloWorldDriver プロジェクトには、次の Windows ポータブル デバイス ファイルが含まれています。

| Filename                | 説明                                                                                                                                                                        |
|-------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| WpdBaseDriver.cpp       | WpdBaseDriver のメンバー関数の実装が含まれています。                                                                                                                  |
| WpdBaseDriver.h         | WpdBaseDriver クラスの定義が含まれています。 このクラスには、メッセージをディスパッチし、ドライバー オブジェクトを初期化され、そのメンバー関数が含まれています。                     |
| WpdCapabilities.cpp     | WpdCapabilities のメンバー関数の実装が含まれています。                                                                                                                |
| WpdCapabilities.h       | WpdCapabilities クラスの定義が含まれています。 このクラスには取得するためのイベント ハンドラーが含まれています: サポートされているコマンド、コマンド オプション、関数のカテゴリとなどです。 |
| WpdObjectEnum.cpp       | WpdObjectEnumerator クラスの実装が含まれています。                                                                                                                       |
| WpdObjectEnum.h         | WpdObjectEnumerator クラスの定義が含まれています。 このクラスには、デバイスでサポートされているオブジェクトを列挙するメンバー関数が含まれています。                                |
| WpdObjectProperties.cpp | WpdObjectProperties クラスの実装が含まれています。                                                                                                                       |
| WpdObjectProperties.h   | WpdObjectProperties クラスの定義が含まれています。 このクラスには、設定し、デバイスでサポートされるプロパティを取得するメンバー関数が含まれています。                      |
| WpdObjectResources.cpp  | WpdObjectResources のメンバー関数の実装が含まれています。                                                                                                             |
| WpdObjectResources.h    | WpdObjectResources クラスの定義が含まれています。 このクラスには、ドライバーによってサポートされているリソースを取得するメンバー関数が含まれています。                              |

 

 

 




