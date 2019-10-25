---
title: コンテキストの解放
description: コンテキストの解放
ms.assetid: e2b87662-c1bd-45a7-82a3-29817f7692fc
keywords:
- コンテキスト WDK ファイルシステムミニフィルター、解放
- コンテキストの解放
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8130c31ee714110e6398f70b004706472ff6ee3a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841330"
---
# <a name="freeing-contexts"></a>コンテキストの解放


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


コンテキストは削除された後に解放され、未処理のすべての参照が解放されます。

この規則には例外が1つあります。コンテキストが作成されているものの、 **FltSet***Xxx***コンテキスト**を呼び出すことによって設定されていない場合は、削除する必要はありません。 参照カウントが0になると解放されます。 ([コンテキストの解放](releasing-contexts.md)に関するコード例を参照してください)。

ミニフィルタードライバーによってそのコンテキスト型が登録されると、コンテキストが解放される前に呼び出されるコンテキストクリーンアップコールバックルーチンを各コンテキスト定義に含めることができます。 詳細については、「 [**PFLT\_CONTEXT\_CLEANUP\_CALLBACK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_context_cleanup_callback)」を参照してください。

 

 




