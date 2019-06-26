---
title: フィルター モジュールのデタッチ
description: フィルター モジュールのデタッチ
ms.assetid: ef987f2f-a681-4ddb-959a-1becdf633678
keywords:
- WDK のモジュールをフィルター処理したり、ネットワーク
- フィルター モジュールのデタッチ
- フィルター ドライバー WDK ネットワークは、フィルター モジュールのデタッチ
- NDIS フィルター ドライバー WDK、フィルター モジュールのデタッチ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8b1f61ee168262c4a1cb44d945ba8028a286e90
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381437"
---
# <a name="detaching-a-filter-module"></a>フィルター モジュールのデタッチ





NDIS フィルター ドライバーの呼び出しのドライバー スタックからフィルター モジュールをデタッチ プロセスを開始する[ *FilterDetach* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_detach)関数。 実行の開始時、 *FilterDetach*関数の場合、フィルター モジュールが入力、 *Detached*状態。 フィルター モジュールをデタッチする前に NDIS ドライバー スタックを一時停止する必要があります。 ドライバー スタックを一時停止の詳細については、次を参照してください。[ドライバー スタックを一時停止](pausing-a-driver-stack.md)します。

その*FilterDetach*関数の場合、ドライバーは、そのコンテキスト領域と、影響を受けるフィルター モジュール (バッファー プール) などその他のリソースを解放します。 フィルター ドライバーに呼び出しが失敗することはできません*FilterDetach*します。 そのため、フィルター ドライバーが事前割り当てを行う、アタッチ操作中にデタッチ操作を正常に実行するために必要なすべてのリソース。 フィルター モジュールのインポートに関する詳細については、次を参照してください。[フィルター モジュールのアタッチ](attaching-a-filter-module.md)します。

フィルターの後、モジュールがから返す*FilterDetach*、NDIS ドライバーの一時停止したスタックを開始できます。 ドライバー スタックを起動する方法の詳細については、次を参照してください。[開始ドライバー スタック](starting-a-driver-stack.md)します。

 

 





