---
title: NDIS 6.30、ドライバーのコンパイル
description: このセクションは、NDIS 6.30 ドライバーをコンパイルする方法を説明します
ms.assetid: 6CBAFAA2-7DA3-4184-B82B-AEFF61F7072C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f286af8e981b57abb6175b5599c5ed1634a6ae92
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379279"
---
# <a name="compiling-an-ndis-630-driver"></a>NDIS 6.30 ドライバーのコンパイル


Windows 8 のリリースの Windows Driver Kit (WDK) では、ドライバーの開発環境は、Visual Studio に統合されます。 コーディング、ビルド、テスト、デバッグ、展開、およびドライバーを解放するのに必要なツールのほとんどは、Visual Studio のユーザー インターフェイスでは使用できます。 これは、ドライバーのライフ サイクルのさまざまな段階がスタンドアロンのツールを使用して別のタスクとして実行された、WDK の以前のリリースから出発地です。

Windows 8 の WDK には、ヘッダー バージョン管理がサポートしています。 ヘッダー バージョン管理は、NDIS 6.30 ドライバーがコンパイル時に適切な NDIS 6.30 データ構造を使用することを確認します。 ドライバーの Visual Studio プロジェクトには、次のコンパイラ設定を追加します。

-   ミニポート ドライバーでは、追加 NDIS630\_ミニポート = 1。

-   フィルターまたはプロトコル ドライバーでは、追加 NDIS630 = 1。

WDK の Windows 8 のリリースでは、ドライバーをビルドする方法の詳細については、次を参照してください。[ドライバーをビルド](https://docs.microsoft.com/windows-hardware/drivers/develop/building-a-driver)します。

ドライバーのビルド ファイルを Visual Studio プロジェクトに変換する方法の詳細については、次を参照してください。 [、ドライバーから既存のソース ファイルを作成する](https://docs.microsoft.com/windows-hardware/drivers)します。

 

 





