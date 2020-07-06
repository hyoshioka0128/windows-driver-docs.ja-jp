---
title: 無線マネージャー ファイル一覧
description: 次の表では、ラジオマネージャー DLL に含まれるファイルについて説明します。
ms.assetid: 70A8B11F-89FF-49E3-933E-2BB66D5E1BF6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b34c2d6280e0fffbceff58fa1b4be38e6deea0d1
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968265"
---
# <a name="the-radio-manager-file-list"></a>無線マネージャー ファイル一覧

> [!IMPORTANT] 
> Windows 8.1 のこのドキュメントと位置情報ドライバーのサンプルは、非推奨とされました。

次の表では、ラジオマネージャー DLL に含まれるファイルについて説明します。

**ファイル名**: 内容

**SampleRM**: サンプルのラジオマネージャー dll をビルドするための Visual Studio 2010 ソリューションファイル

**sampleRM**: サンプルのラジオマネージャーのインターフェイス定義

**RadioMgr**: Windows ラジオマネージャーのインターフェイス定義

**SampleRadioManager**: ラジオマネージャーに必要な関数のヘッダーファイル

**SampleRadioInstance**: Radio インスタンスに必要な関数のヘッダーファイル

**SampleInstanceCollection**: ラジオインスタンスのコレクションに必要な関数のヘッダーファイル

**precomp .h**: 共通ヘッダーファイル

**dllmain**: 標準の dllmain

**Internalinterfaces .h**: このサンプルで使用される内部インターフェイスのヘッダーファイル

**SampleRadioManager**: サンプルのラジオマネージャーの実装の詳細。 重要な概念は次のとおりです:-IMediaRadioManagerNotifySink を使用したラジオインスタンスイベント-ラジオインスタンスの追加/削除-システムイベントのワーカージョブのキュー登録と展開

**SampleRadioInstance**: サンプルのラジオインスタンスの実装の詳細。 重要な概念には、-アクセサー & ラジオ情報の修飾子、インスタンス変更関数

**SampleInstanceCollection**: サンプルインスタンスコレクションの実装の詳細。 重要な概念は次のとおりです:-Radio インスタンスの検出と取得

**RadioMgr \_ **: MIDL によって生成されたファイルを含めるヘルパーソースファイル。


 

 

 




