---
title: コンテキストの解放
description: コンテキストの解放
ms.assetid: e2b87662-c1bd-45a7-82a3-29817f7692fc
keywords:
- WDK のコンテキストのファイル システム ミニフィルターを解放します。
- コンテキストを解放します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9100a9bf404c94bc6ec92ca74bdf7cf46a2b78c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384569"
---
# <a name="freeing-contexts"></a>コンテキストの解放


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


コンテキストは、削除されへの参照がすべて未処理がリリースされた後に解放されます。

このルールを 1 つの例外: コンテキストが作成されましたが、呼び出すことによって設定されていないかどうかは**FltSet***Xxx***コンテキスト**、削除する必要はありません。 参照カウントがゼロになったときに解放されます。 (のコード例を参照してください[解放コンテキスト](releasing-contexts.md)。)。

ミニフィルター ドライバーでは、そのコンテキストの種類を登録、各コンテキストの定義は必要に応じて、コンテキストが解放される前に呼び出されるコンテキスト クリーンアップ コールバック ルーチンを含めることができます。 詳細については、次を参照してください。 [ **PFLT\_コンテキスト\_クリーンアップ\_コールバック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_context_cleanup_callback)します。

 

 




