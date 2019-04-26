---
title: コンパイル、NDIS 6.40 ドライバー
description: このセクションは、NDIS 6.40 ドライバーをコンパイルする方法を説明します
ms.assetid: AF027939-06C7-435C-90D9-82272CED6A84
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e4d0cba0a654d8e9f6996f63e103ec601fcd0da0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344251"
---
# <a name="compiling-an-ndis-640-driver"></a>NDIS 6.40 ドライバーのコンパイル


Windows 8.1 の WDK には、ヘッダー バージョン管理がサポートされています。 ヘッダー バージョン管理は、NDIS 6.40 ドライバーがコンパイル時に適切な NDIS 6.40 データ構造を使用することを確認します。

ドライバーの Visual Studio プロジェクトには、次のコンパイラ設定を追加します。

-   ミニポート ドライバーでは、追加 NDIS640\_ミニポート = 1。

-   フィルターまたはプロトコル ドライバーでは、追加 NDIS640 = 1。

WDK の Windows 8.1 のリリースでは、ドライバーをビルドする方法の詳細については、次を参照してください。[ドライバーをビルド](https://msdn.microsoft.com/windows-drivers/develop/building_a_driver)します。

ドライバーのビルド ファイルを Visual Studio プロジェクトに変換する方法の詳細については、次を参照してください。 [、ドライバーから既存のソース ファイルを作成する](https://msdn.microsoft.com/windows-drivers/develop/creating_a_driver_from_existing_source_files)します。

 

 





