---
Description: The Windows Driver Frameworks Files
title: Windows ドライバー フレームワーク ファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 745b470dd602b4098587f4a3faf433c14ccff7b3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535482"
---
# <a name="the-windows-driver-frameworks-files"></a>Windows ドライバー フレームワーク ファイル


WpdHelloWorldDriver プロジェクトには、次の Windows ユーザー モード ドライバー フレームワーク (UMDF) ファイルが含まれています。

| Filename   | 説明                                                                                                                                                                   |
|------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Device.cpp | CDevice のメンバー関数の実装が含まれています。 これらの関数は、プラグ アンド プレイし、電源管理イベントを処理します。                                                 |
| Device.h   | CDevice クラスの定義が含まれています。                                                                                                                                  |
| Driver.cpp | CDriver のメンバー関数の実装が含まれています。 これらの関数は、デバイスの初期化とクリーンアップを処理します。                                                         |
| Driver.h   | CDriver クラスの定義が含まれています。                                                                                                                                  |
| Queue.cpp  | CQueue のメンバー関数の実装が含まれています。                                                                                                                    |
| Queue.h    | CQueue クラスの定義と Windows Driver Foundation (WDF) コールバックの定義が含まれています。 これらの関数は、デバイスのコントロールと、ファイルの作成を処理します。 |

 

 

 




