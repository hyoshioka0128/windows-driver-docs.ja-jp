---
title: TraceView ワークスペースの制限事項
description: TraceView ワークスペースの制限事項
ms.assetid: 9c8cad66-251c-473e-b723-aae744b6737a
keywords:
- ワークスペースの WDK traceview で、制限事項
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5045f9a2fdc006215e8639ffb79219e809459928
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579583"
---
# <a name="limitations-of-traceview-workspaces"></a>TraceView ワークスペースの制限事項


Traceview でワークスペースの機能には、次の制限があります。

-   ワークスペースでは、パスとトレース セッションに関連付けられているファイル名が保存されているため、ワークスペースに保存されているファイルが再利用し、ワークスペースを開くたびに上書きされます。 ファイルを保持するためには、移動または各トレース セッションの後に名前を変更します。

-   ワークスペースへの変更は自動的に保存されませんし traceview でプロンプトが表示されません保存するようにします。

-   トレース セッションのグループに含まれているワークスペースを保存することはできません。 詳細については、次を参照してください。[トレース セッションをグループ化](grouping-trace-sessions.md)します。

-   各ワークスペースでは、1 つだけのトレース セッションまたはログの表示を保存できます。 1 つ以上のトレース セッションを保存またはログの表示、トレース セッションのグループを作成します。

-   ワークスペースはファイルに保存されません。 リモート コンピューターには移動できません。

-   Traceview での 1 つのバージョンで作成されたワークスペースは可能性があります traceview での他のバージョンでサポートされていません。

 

 





