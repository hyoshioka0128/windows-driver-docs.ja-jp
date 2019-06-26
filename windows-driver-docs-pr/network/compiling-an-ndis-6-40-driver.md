---
title: コンパイル、NDIS 6.40 ドライバー
description: このセクションは、NDIS 6.40 ドライバーをコンパイルする方法を説明します
ms.assetid: AF027939-06C7-435C-90D9-82272CED6A84
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc799726e830a1da4ed80851fbcd337382629b2e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379267"
---
# <a name="compiling-an-ndis-640-driver"></a>NDIS 6.40 ドライバーのコンパイル


Windows 8.1 の WDK には、ヘッダー バージョン管理がサポートされています。 ヘッダー バージョン管理は、NDIS 6.40 ドライバーがコンパイル時に適切な NDIS 6.40 データ構造を使用することを確認します。

ドライバーの Visual Studio プロジェクトには、次のコンパイラ設定を追加します。

-   ミニポート ドライバーでは、追加 NDIS640\_ミニポート = 1。

-   フィルターまたはプロトコル ドライバーでは、追加 NDIS640 = 1。

WDK の Windows 8.1 のリリースでは、ドライバーをビルドする方法の詳細については、次を参照してください。[ドライバーをビルド](https://docs.microsoft.com/windows-hardware/drivers/develop/building-a-driver)します。

ドライバーのビルド ファイルを Visual Studio プロジェクトに変換する方法の詳細については、次を参照してください。 [、ドライバーから既存のソース ファイルを作成する](https://docs.microsoft.com/windows-hardware/drivers)します。

 

 





