---
Description: COM コンポーネント ファイル
title: COM コンポーネント ファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17655c0df198cc48e4c1c2baeccb871be84e9ffa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380838"
---
# <a name="the-com-component-files"></a>COM コンポーネント ファイル


WpdHelloWorldDriver プロジェクトには、次の COM コンポーネント ファイルが含まれています。

| Filename                | 説明                                                                                                                                               |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| Resource.h              | ドライバーの識別子の 1 つの定義が含まれています。                                                                                                 |
| stdafx.h                | 標準のシステム ファイルが含まれています。                                                                                                                           |
| WpdHelloWorldDriver.cpp | クラス ファクトリ、および DLL エントリ ポイントを取得する、サーバーの登録を処理する基本的な COM メソッドが含まれています。                                       |
| WpdHelloWorldDriver.def | モジュールのパラメーターを宣言します。                                                                                                                           |
| WpdHelloWorldDriver.idl | ドライバーの COM コンポーネントのために必要な定義が含まれています。                                                                                        |
| WpdHelloWorldDriver.rc  | ドライバーで必要なリソースの定義が含まれています。 これらのリソースには、ファイルの種類には、ファイルの説明文字列、元のファイル名が含まれます。 |
| WpdHelloWorldDriver.rgs | ドライバーの COM コンポーネントの登録スクリプトが含まれています。                                                                                          |

 

 

 




