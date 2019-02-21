---
title: 部分的な印刷プロバイダーの概要
description: 部分的な印刷プロバイダーの概要
ms.assetid: 622f99e3-d4a5-42f0-ab71-4d256e0ea02c
keywords:
- WDK、部分的な印刷プロバイダーのプロバイダーを印刷します。
- ネットワーク印刷プロバイダー WDK、部分的な印刷プロバイダー
- 部分的な印刷プロバイダー WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4115664165373c56a771180dad0187f65636830
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560021"
---
# <a name="overview-of-partial-print-providers"></a>部分的な印刷プロバイダーの概要





部分的なプロバイダーの DLL は、通常プロバイダー関数のみを印刷キューを管理し、印刷ジョブのカスタマイズされたバージョンを実装します。 部分的なプロバイダーは、印刷クライアント システムでのみを実行しとプリンターのデータを生成するためのドライバーの管理操作は、ローカルの印刷プロバイダーによって異なります。 複数の部分的なプロバイダーは、クライアント システムに存在できます。

[関数は、印刷プロバイダーによって定義されている](functions-defined-by-print-providers.md)、特定の関数が識別される"required"として。 部分的な印刷プロバイダーは、必要なすべての機能を提供する必要があります。 部分的な印刷プロバイダー一般的には実装されません省略可能な関数のいずれか。 必要な関数は、次の関数グループに属します。

[初期化関数](functions-defined-by-print-providers.md#ddk-initialization-function-gg)

[印刷キューの管理機能](functions-defined-by-print-providers.md#ddk-print-queue-management-functions-gg)

[印刷ジョブの作成機能](functions-defined-by-print-providers.md#ddk-print-job-creation-functions-gg)

[印刷ジョブのスケジュールの機能](functions-defined-by-print-providers.md#ddk-print-job-scheduling-functions-gg)

[ポートの管理機能](functions-defined-by-print-providers.md#ddk-port-management-functions-gg)

部分的な印刷プロバイダー、印刷キューに相当するプリンター ポートを検討してください。 プリンターを受け取る関数の\_情報\_(Microsoft Windows SDK のドキュメントで説明) 2 つの構造体、構造体の**サポート**メンバーは、印刷キュー名を設定する必要があります。 したがって、印刷キュー名がある場合\\ \\Server\\printer1 は通常、ポート名も必要\\\\サーバー\\printer1 は通常します。 ポートの名前を返す必要があります (Windows SDK のドキュメントで説明) EnumPorts の部分的な印刷プロバイダーの実装\\ \\Server\\printer1 は通常します。

」の説明に従って[印刷プロバイダーの概要について](introduction-to-print-providers.md)、アプリケーションの呼び出しを**ようになりました**スプーラーのルーターをいずれかの指定した印刷キューを認識するまで、各印刷プロバイダーを呼び出すと、ハンドルを返します。

部分的な印刷プロバイダーがローカルのプロバイダーを置き換えられないことに注意してください。 プリンターへの接続をユーザーが作成されたら、プロバイダー関数に対する各呼び出しは、呼び出し自体を処理または部分的なプロバイダーへの経路をローカルのプロバイダーを介してルーティングされます。 プロバイダーの関数は、"required"として識別されるすべての呼び出しは、ローカルのプロバイダーから、適切な部分のプロバイダーにルーティングされます。

部分的なプロバイダーが印刷ジョブを生成しません。ローカルのプロバイダーに依存しているとその*プリント プロセッサ*を作成する[生データ](raw-data-type.md)をプリンターに送信できます。 プリント プロセッサが、ローカルのプロバイダーを呼び出すと**StartDocPrinter**関数 (を参照してください[印刷ジョブを印刷](printing-a-print-job.md))、印刷キューが部分プロバイダーによってサポートされている部分に、ローカルのプロバイダーは、プロバイダーの**StartDocPrinter** (ファイル) としての生データを提供する関数。 部分的なプロバイダーの**StartDocPrinter**、 **WritePrinter**、および**EndDocPrinter**関数は、ネットワーク経由で生データをリモート印刷キューに送信する必要があります。

 

 




