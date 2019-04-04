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
ms.openlocfilehash: 77fb90910cf888b6f29071e72168a0b99ee6b732
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532810"
---
# <a name="detaching-a-filter-module"></a>フィルター モジュールのデタッチ





NDIS フィルター ドライバーの呼び出しのドライバー スタックからフィルター モジュールをデタッチ プロセスを開始する[ *FilterDetach* ](https://msdn.microsoft.com/library/windows/hardware/ff549918)関数。 実行の開始時、 *FilterDetach*関数の場合、フィルター モジュールが入力、 *Detached*状態。 フィルター モジュールをデタッチする前に NDIS ドライバー スタックを一時停止する必要があります。 ドライバー スタックを一時停止の詳細については、[ドライバー スタックを一時停止](pausing-a-driver-stack.md)を参照してください。

その*FilterDetach*関数の場合、ドライバーは、そのコンテキスト領域と、影響を受けるフィルター モジュール (バッファー プール) などその他のリソースを解放します。 フィルター ドライバーに呼び出しが失敗することはできません*FilterDetach*します。 そのため、フィルター ドライバーが事前割り当てを行う、アタッチ操作中にデタッチ操作を正常に実行するために必要なすべてのリソース。 フィルター モジュールのインポートに関する詳細については、[フィルター モジュールのアタッチ](attaching-a-filter-module.md)を参照してください。

フィルターの後、モジュールがから返す*FilterDetach*、NDIS ドライバーの一時停止したスタックを開始できます。 ドライバー スタックを起動する方法の詳細については、[開始ドライバー スタック](starting-a-driver-stack.md)を参照してください。

 

 





