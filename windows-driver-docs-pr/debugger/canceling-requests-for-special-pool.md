---
title: 特別なプールの要求の取り消し
description: 特別なプールの要求の取り消し
ms.assetid: fb18cb15-33ee-4e6d-856e-70c4ffbf8383
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d19940f4cc708eb9421d8641aa75554ba92c273
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375147"
---
# <a name="canceling-requests-for-special-pool"></a>特別なプールの要求の取り消し


## <span id="ddk_canceling_requests_for_special_pool_dtools"></span><span id="DDK_CANCELING_REQUESTS_FOR_SPECIAL_POOL_DTOOLS"></span>


GFlags を使用すると、GFlags を使用して、要求が行われた場合は、特別なプールから割り当ての要求をキャンセルします。 Driver Verifier を使用して作成された特別なプールの要求をキャンセルするのに GFlags を使用することはできません。

Windows Vista および以降のバージョンの Windows では、特別なプールの要求をキャンセルするのにコマンドラインを使用することもできます。 詳しくは、次を参照してください。 [ **GFlags コマンド**](gflags-commands.md)します。

**特別なプールの要求をキャンセルするには**

1.  システム レジストリ タブまたは フラグ タブを選択します。

    Windows Vista と Windows の以降のバージョンでは、このオプションは両方のタブで使用します。 以前のバージョンの Windows では、上でのみ使用できますが、**システム レジストリ**タブ。

2.  テキストまたは 16 進数の値を削除、**カーネル特別なプール タグ**ボックス。

3.  **[適用]** をクリックします。

 

 





