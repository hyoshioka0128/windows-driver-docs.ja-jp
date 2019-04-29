---
title: 無線マネージャー ファイル一覧
description: 次の表では、無線マネージャー DLL 内にあるファイルについて説明します。
ms.assetid: 70A8B11F-89FF-49E3-933E-2BB66D5E1BF6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42e3ca5785a317105ef72ccd189af999e9b1d15f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63326174"
---
# <a name="the-radio-manager-file-list"></a>無線マネージャー ファイル一覧

> [!IMPORTANT] 
> このドキュメントと Windows 8.1 の地理的位置情報ドライバー サンプルが非推奨とされました。

次の表では、無線マネージャー DLL 内にあるファイルについて説明します。

|                              |                                                                                                                                                                                                                                             |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ファイル名                    | 目次                                                                                                                                                                                                                                    |
| SampleRM.sln                 | サンプルのラジオ マネージャー dll を構築するための Visual Studio 2010 ソリューション ファイル                                                                                                                                                              |
| sampleRM.idl                 | インターフェイス定義のサンプル ラジオ マネージャー                                                                                                                                                                                       |
| RadioMgr.idl                 | Windows ラジオ マネージャー用のインターフェイス定義                                                                                                                                                                                        |
| SampleRadioManager.h         | ラジオ マネージャー用に必要な関数のヘッダー ファイル                                                                                                                                                                                  |
| SampleRadioInstance.h        | ラジオ インスタンスに必要な関数のヘッダー ファイル                                                                                                                                                                                 |
| SampleInstanceCollection.h   | ラジオ インスタンス コレクションのために必要な関数のヘッダー ファイル                                                                                                                                                                  |
| precomp.h                    | 共通のヘッダー ファイル                                                                                                                                                                                                                          |
| dllmain.cpp                  | 標準 dllmain                                                                                                                                                                                                                            |
| InternalInterfaces.h         | このサンプルで使用される内部のインターフェイスのヘッダー ファイル                                                                                                                                                                                     |
| SampleRadioManager.cpp       | 実装の詳細のサンプル ラジオ マネージャー。 重要な概念が含まれます: - IMediaRadioManagerNotifySink を利用するラジオ インスタンス イベントの追加/削除ラジオ インスタンス - キューとシステムのイベントの worker ジョブを展開します。 |
| SampleRadioInstance.cpp      | 実装の詳細については、サンプルのラジオ インスタンス。 重要な概念が含まれます: - アクセサー & 無線情報の修飾子のインスタンスを変更する関数                                                                                 |
| SampleInstanceCollection.cpp | 実装の詳細については、サンプルのインスタンスのコレクション。 重要な概念が含まれます:-ラジオ インスタンスの検出と取得                                                                                                             |
| RadioMgr\_interface.cpp      | MIDL で生成されたファイルをインクルードするヘルパー ソース ファイルです。                                                                                                                                                                                     |

 

 

 




