---
title: コンテキストの参照
description: コンテキストの参照
ms.assetid: 9ac3aedb-e057-4e19-9de5-709311072b09
keywords:
- コンテキスト WDK ファイルシステムミニフィルター、参照
- コンテキストの参照
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ef9ab23d9bca46999ad8673292a7a2aa53721cd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841013"
---
# <a name="referencing-contexts"></a>コンテキストの参照


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


フィルターマネージャーでは、参照カウントを使用してミニフィルタードライバーコンテキストの有効期間を管理します。 参照カウントは、コンテキストの状態を示す数値です。 コンテキストが作成されるたびに、コンテキストの参照カウントが1つに初期化されます (これはコンテキストへの最初の参照と呼ばれます)。 システムコンポーネントによってコンテキストが参照されるたびに、コンテキストの参照カウントが1ずつインクリメントされます。 コンテキストが不要になった場合は、その参照カウントがデクリメントされます。 正の参照カウントは、コンテキストが使用可能であることを意味します。 参照カウントがゼロになると、コンテキストは使用できなくなり、フィルターマネージャーによって最終的に解放されます。

通常、コンテキストへの最初の参照は、オブジェクトが破棄されるときに解放されます。 ただし、ミニフィルタードライバーがオブジェクトからコンテキストを削除する必要がある場合、ミニフィルタードライバーは、コンテキストへの最初の参照を解放する必要があります。 コンテキストへの最初の参照を安全に解放するために、ミニフィルタードライバーは[**Fltdeletecontext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdeletecontext)を呼び出します。

ミニフィルタードライバーは、 [**Fltreferencecontext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreferencecontext)を呼び出してコンテキストの参照カウントをインクリメントすることによって、コンテキストに独自の参照を追加できます。 この追加された参照は、最終的に[**FltReleaseContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreleasecontext)を呼び出すことによって削除する必要があります。

 

 




