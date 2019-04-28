---
Description: Windows Driver Framework ファイル
title: Windows Driver Framework ファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 745b470dd602b4098587f4a3faf433c14ccff7b3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378200"
---
# <a name="the-windows-driver-frameworks-files"></a>Windows Driver Framework ファイル


WpdHelloWorldDriver プロジェクトには、次の Windows ユーザー モード ドライバー フレームワーク (UMDF) ファイルが含まれています。

| Filename   | 説明                                                                                                                                                                   |
|------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Device.cpp | CDevice のメンバー関数の実装が含まれています。 これらの関数は、プラグ アンド プレイし、電源管理イベントを処理します。                                                 |
| Device.h   | CDevice クラスの定義が含まれています。                                                                                                                                  |
| Driver.cpp | CDriver のメンバー関数の実装が含まれています。 これらの関数は、デバイスの初期化とクリーンアップを処理します。                                                         |
| Driver.h   | CDriver クラスの定義が含まれています。                                                                                                                                  |
| Queue.cpp  | CQueue のメンバー関数の実装が含まれています。                                                                                                                    |
| Queue.h    | CQueue クラスの定義と Windows Driver Foundation (WDF) コールバックの定義が含まれています。 これらの関数は、デバイスのコントロールと、ファイルの作成を処理します。 |

 

 

 




