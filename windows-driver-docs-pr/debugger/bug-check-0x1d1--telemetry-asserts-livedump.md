---
title: バグ チェック 0x1D1 TELEMETRY_ASSERTS_LIVEDUMP
description: TELEMETRY_ASSERTS_LIVEDUMP のバグ チェックでは、0x000001D1 の値を持ちます。
keywords:
- バグ チェック 0x1D1 TELEMETRY_ASSERTS_LIVEDUMP
- TELEMETRY_ASSERTS_LIVEDUMP
ms.date: 04/19/2018
topic_type:
- apiref
api_name:
- TELEMETRY_ASSERTS_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 83a9e7c9ef598a29a9d303ca6e6b89004fc3c235
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519663"
---
# <a name="bug-check-bug-check-0x1d1-telemetryassertslivedump"></a>チェックのバグ チェック 0x1D1 をバグします。テレメトリ\_アサート\_LIVEDUMP

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


TELEMETRY_ASSERTS_LIVEDUMP のバグ チェックでは、0x000001D1 の値を持ちます。 

製品利用統計情報をアサート検証が失敗しました。

このコードは、実際のバグチェック; には使用しません。デバイスのテレメトリなどを含むライブのダンプを識別するために使用されます。

この問題をトラブルシューティングするには、MICROSOFT_TELEMETRY_ASSERT(expression) 内の式が有効な理由を確認する呼び出し履歴を検査します。

## <a name="telemetryassertslivedump-parameters"></a>テレメトリ\_アサート\_LIVEDUMP パラメーター

パラメーター | 説明 
|---------|--------------|
1 | Rva
2 | ModuleName
3 | TimeStamp
4 | SizeOfImage

 

 




