---
title: 分類コールアウトの処理
description: 分類コールアウトの処理
ms.assetid: 284aeda0-8275-440f-abf4-84a0c61cc4f4
keywords:
- Windows フィルタリングプラットフォームコールアウトドライバー WDK、分類コールアウト
- コールアウトドライバー WDK Windows フィルタリングプラットフォーム、コールアウトの分類
- Classid (場合)
- コールアウトの分類 WDK Windows フィルタリングプラットフォーム
- コールアウトの分類 WDK Windows フィルタリングプラットフォーム、コールアウトの分類について
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb25beb1535a6b25b51f9c84fe3e5de6041a49dd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843489"
---
# <a name="processing-classify-callouts"></a>分類コールアウトの処理


フィルターエンジンは、コールアウトによって処理されるネットワークデータがある場合に、コールアウトの[*classid*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn0)関数を呼び出します。 これは、フィルターのアクションのコールアウトを指定するフィルターに対して、すべてのフィルター条件が true である場合に発生します。 このようなフィルターにフィルター条件が含まれていない場合、フィルターエンジンは常にコールアウトの*classid*関数を呼び出します。

フィルターエンジンは、複数の異なるデータ項目をコールアウトの*classid*関数に渡します。 これらのデータ項目には、固定データ値、メタデータ値、生のネットワークデータ、フィルター情報、およびすべてのフローコンテキストが含まれます。 フィルターエンジンがコールアウトに渡す特定のデータ項目は、特定のフィルター処理レイヤーと、 *classid*が呼び出される条件によって異なります。 分類*関数は*、これらのデータ項目の任意の組み合わせを使用して、フィルターの決定を行うことができます。

コールアウトの*classid*関数の実装は、コールアウトがどのように設計されているかによって異なります。 次のセクションでは、コールアウトの一般的な関数の例を紹介します。

[詳細な検査にコールアウトを使用する](using-a-callout-for-deep-inspection.md)

[コールアウトを使用したストリームデータの詳細な検査](using-a-callout-for-deep-inspection-of-stream-data.md)

[パケットおよびストリームデータの検査](inspecting-packet-and-stream-data.md)

[ストリームデータの変更](modifying-stream-data.md)

[データのログ記録](data-logging.md)

[コンテキストとデータフローの関連付け](associating-context-with-a-data-flow.md)

[コールアウトを非同期に分類する処理](processing-classify-callouts-asynchronously.md)

[バインドまたは接続リダイレクトの使用](using-bind-or-connect-redirection.md)

[ALE エンドポイントの有効期間の管理](ale-endpoint-lifetime-management.md)

[パケットタグ付けの使用](using-packet-tagging.md)

特定のコールアウトの*classid*関数の実際の実装は、これらの例の組み合わせに基づいて作成できます。

データフローをサポートするフィルター処理レイヤーでデータを処理するコールアウトの場合、コールアウトの*classid*関数は、コンテキストを各データフローに関連付けることができます。 *Classid*は、このコンテキストを使用して、そのデータフローのフィルターエンジンによって次回呼び出されたときの状態情報を保存できます。 コールアウト関数がコンテキストをデータフローに関連付ける方法の詳細については、「[コンテキストとデータフローの関連付け](associating-context-with-a-data-flow.md)」を参照してください。

WFP は、 *classid*関数の非同期処理をサポートしています。 非同期処理の詳細については、「[プロセス分類のコールアウトを非同期に処理](processing-classify-callouts-asynchronously.md)する」を参照してください。

 

 





