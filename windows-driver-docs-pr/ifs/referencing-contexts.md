---
title: コンテキストの参照
description: コンテキストの参照
ms.assetid: 9ac3aedb-e057-4e19-9de5-709311072b09
keywords:
- WDK のコンテキストのファイル システム ミニフィルターを参照します。
- 参照元のコンテキスト
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 33d5010dc4197c856c67630ca48fd0fd5ce4a863
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385138"
---
# <a name="referencing-contexts"></a>コンテキストの参照


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


フィルター マネージャーは、参照カウント ミニフィルター ドライバーのコンテキストの有効期間の管理を使用します。 参照カウントは、コンテキストの状態を示す数値です。 コンテキストが作成されるは、コンテキストの参照カウントが 1 つ (コンテキストへの初期の参照と呼ばれます) に初期化されます。 コンテキストがシステム コンポーネントによって参照されるたびに、コンテキストの参照カウントが 1 ずつインクリメントされます。 コンテキストが不要になったときに、参照カウントは減少します。 正の値の参照カウントは、コンテキストが使用可能なことを意味します。 参照カウントがゼロになったら、コンテキストが使用可能なおよびフィルター マネージャーが最終的に解放します。

オブジェクトが破棄とコンテキストへの初期の参照は、通常は解放されます。 ただし、ミニフィルター ドライバーでは、オブジェクトからコンテキストを削除する必要があります、ミニフィルター ドライバーにコンテキストにその最初の参照が解放何らかの理由で必要があります。 ミニフィルター ドライバーの呼び出しコンテキストにその最初の参照を安全に解放する[ **FltDeleteContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltdeletecontext)します。

ミニフィルター ドライバーが呼び出すことによって、コンテキストに独自の参照を追加できます[ **FltReferenceContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltreferencecontext)コンテキストの参照カウントをインクリメントします。 これは、追加の参照は、呼び出すことによって最終的に削除する必要があります[ **FltReleaseContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltreleasecontext)します。

 

 




