---
title: 欠陥のトレースの保存
description: Static Driver Verifier の欠陥のトレースの保存
ms.assetid: 6d54a532-75ff-4226-86a7-cdc2046b0b5b
keywords:
- Static Driver Verifier WDK、Static Driver Verifier のレポート
- StaticDV WDK、Static Driver Verifier のレポート
- SDV の WDK、Static Driver Verifier のレポート
- 静的ドライバー検証ツールの WDK、エラーの検索
- StaticDV WDK、エラーの検索
- SDV の WDK、エラーの検索
- エラー WDK Static Driver Verifier の検索
- エラー WDK Static Driver Verifier
- WDK Static Driver Verifier をエクスポートします。
- Static Driver Verifier レポート WDK
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a78b986f520a84f92fc3ba40ea8d38d61112e61e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340257"
---
# <a name="saving-defect-traces"></a>欠陥のトレースの保存

静的ドライバー検証ツールの参加を解除ビューアーは、特定の欠陥のトレースを簡単に共有可能な形式で保存できるようにする機能を持ちます。  

トレースを保存するには、次のように選択します"として保存します."。ファイル メニュー、または ctrl キーを押し S キーを押します  

![保存先の場所を示す、欠陥のビューアー ウィンドウのスクリーン ショット機能](images/sdv-savedefecttrace.png)

トレース フォルダー ("sdvdefect") を配置するフォルダーを指定します。

保存された欠陥トレースは、関連するソース コード、欠陥は、トレースと SDV に必要なファイル、トレースを表示するには、実行可能ファイルのコピーが格納されます。  トレースを表示するには、sdvdefect.exe ファイルをダブルクリックします。

