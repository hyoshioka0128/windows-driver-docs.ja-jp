---
title: 印刷スプーラー アーキテクチャ
description: 印刷スプーラー アーキテクチャ
ms.assetid: 712da599-29cb-4df9-9627-49907f0aa500
keywords:
- WDK 印刷スプーラーのアーキテクチャ
- 印刷スプーラ アーキテクチャ WDK
- WDK のジョブの印刷、印刷スプーラー
- WDK のジョブの印刷、印刷スプーラー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5bf65d0edf49f9f3ffe0df4441e58915ada3f1ed
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573876"
---
# <a name="print-spooler-architecture"></a>印刷スプーラー アーキテクチャ





Microsoft Windows 2000 およびそれ以降の印刷スプーラーは、Microsoft が提供し、省略可能なベンダーから提供された、コンポーネントの責任を負うが含まれる一連は構成されています。

-   ローカルまたはネットワーク上に印刷ジョブを処理するかどうかを決定します。

-   特定の種類のプリンターで出力用のプリンター ドライバーと組み合わせて、GDI によって作成されたデータ ストリームを受け入れます。

-   (スプールが有効になっている) 場合は、データをファイルにスプールされています。

-   論理プリンター キュー内の最初の使用可能な物理プリンターを選択します。

-   スプール形式からデータ ストリームを変換する (など*拡張メタファイル (EMF)*) プリンター ハードウェアに送信できる形式に (など*プリンター制御言語 (PCL)*)。

-   プリンターのハードウェアへのデータ ストリームを送信します。

-   レジストリ ベースのデータベースを維持する[スプーラー コンポーネント](spooler-components.md)と[プリンター フォーム](printer-forms-support.md)します。

-   (Windows Vista)プリント サーバー上ではなく、クライアント コンピューター上の印刷ジョブを表示します。 [クライアント側のレンダリング](client-side-rendering.md)プリント サーバーのワークロードを容易に、印刷ドライバーに透過的であり Windows Vista では既定で有効です。

-   Windows 7 では、印刷ドライバーは、スプーラーから別のプロセスで実行できます。 この機能は呼[プリンター ドライバーの分離](printer-configuration.md)します。

 

 




