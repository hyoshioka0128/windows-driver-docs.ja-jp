---
title: 分類コールアウトの処理
description: 分類コールアウトの処理
ms.assetid: 284aeda0-8275-440f-abf4-84a0c61cc4f4
keywords:
- Windows Filtering Platform コールアウト ドライバー WDK、コールアウトを分類します。
- コールアウト ドライバー WDK Windows フィルタ リング プラットフォームのコールアウトを分類します。
- classifyFn
- WDK Windows フィルタ リング プラットフォームのコールアウトを分類します。
- WDK Windows フィルタ リング プラットフォームのコールアウトの分類、コールアウトを約分類する.
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dda31876f745df486aee716a996b5ecf2c4b46d4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385482"
---
# <a name="processing-classify-callouts"></a>分類コールアウトの処理


フィルター エンジン呼び出し吹き出しの[ *classifyFn* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nc-fwpsk-fwps_callout_classify_fn0)引き出し線によって処理されるネットワーク データがある場合は吹き出し関数。 これは、フィルターのアクションの引き出し線を指定するフィルターのフィルター処理のすべての条件が当てはまる場合に発生します。 このようなフィルターがフィルター条件を持たない場合、フィルター エンジンを常に呼び出します吹き出しの*classifyFn*コールアウト関数。

フィルター エンジンでは、いくつかの異なるデータ アイテムを渡すには、吹き出しの*classifyFn*コールアウト関数。 これらのデータ項目には、固定のデータ値、メタデータの値、未加工のネットワーク データ、フィルターについては、および任意のコンテキストのフローが含まれます。 フィルター エンジンは吹き出しに渡される特定のデータ項目は、特定のフィルタ リング層とする条件によって異なります。 *classifyFn*が呼び出されます。 A *classifyFn*関数は、これらのデータ項目の任意の組み合わせを使用して、そのフィルターの決定を行います。

吹き出しの実装*classifyFn*コールアウト関数は吹き出しが実行するように設計に依存します。 次のセクションでは、コールアウトのより一般的な機能のいくつかの例を示します。

[詳細な検査のコールアウトを使用してください。](using-a-callout-for-deep-inspection.md)

[Stream のデータの詳細な検査のコールアウトを使用してください。](using-a-callout-for-deep-inspection-of-stream-data.md)

[パケットと Stream のデータを調べる](inspecting-packet-and-stream-data.md)

[Stream のデータの変更](modifying-stream-data.md)

[データのログ記録](data-logging.md)

[データ フローとコンテキストの関連付け](associating-context-with-a-data-flow.md)

[処理がコールアウトを非同期的に分類します。](processing-classify-callouts-asynchronously.md)

[Bind を使用して、またはリダイレクトの接続](using-bind-or-connect-redirection.md)

[ALE エンドポイントの有効期間管理](ale-endpoint-lifetime-management.md)

[パケットがタグ付けを使用してください。](using-packet-tagging.md)

特定のコールアウトの実際の実装*classifyFn*コールアウト関数は、これらの例の組み合わせに基づくことができます。

コールアウトのプロセスのデータをフィルター処理には層をサポートでデータ フローまで、引き出し線の*classifyFn*コールアウト関数は、各データ フローでコンテキストを関連付けることができます。 *ClassifyFn*関数は、このコンテキストを使用して、そのデータ フローのフィルター エンジンによって呼び出されたときに [次へ] に状態情報を保存します。 吹き出し関数がデータ フローでコンテキストを関連付けることができる方法の詳細については、次を参照してください。[データ フローに関連付けるコンテキスト](associating-context-with-a-data-flow.md)します。

WFP の非同期処理をサポートしている、 *classifyFn*コールアウト関数。 非同期処理の詳細については、次を参照してください。[分類コールアウト非同期を処理](processing-classify-callouts-asynchronously.md)します。

 

 





