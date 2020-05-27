---
title: バグチェック 0x1D1 TELEMETRY_ASSERTS_LIVEDUMP
description: TELEMETRY_ASSERTS_LIVEDUMP のバグチェックには、0x000001D1 という値があります。
keywords:
- バグチェック 0x1D1 TELEMETRY_ASSERTS_LIVEDUMP
- TELEMETRY_ASSERTS_LIVEDUMP
ms.date: 04/19/2018
topic_type:
- apiref
api_name:
- TELEMETRY_ASSERTS_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 66fdc0b2c6d5792b4ecd9acb40e3e1727dcd844b
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851265"
---
# <a name="bug-check-0x1d1-telemetry_asserts_livedump"></a>バグチェック 0x1D1: テレメトリ \_ アサート \_ LIVEDUMP

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


TELEMETRY_ASSERTS_LIVEDUMP のバグチェックには、0x000001D1 という値があります。 

テレメトリアサートの検証に失敗しました。

このコードは、実際のバグチェックには使用できません。これは、デバイステレメトリを含むライブダンプを識別するために使用されます。

この問題のトラブルシューティングを行うには、呼び出し履歴を調べて、MICROSOFT_TELEMETRY_ASSERT (式) の式が無効である理由を確認します。

## <a name="telemetry_asserts_livedump-parameters"></a>テレメトリ \_ アサート \_ LIVEDUMP パラメーター

パラメーター | 説明 
|---------|--------------|
1 | Rva
2 | ModuleName
3 | TimeStamp
4 | SizeOfImage

 

 




