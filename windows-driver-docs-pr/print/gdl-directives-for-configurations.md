---
title: 構成の GDL ディレクティブ
description: 構成の GDL ディレクティブ
ms.assetid: c7b3c364-06b2-4de8-9fe6-2c77d313a2f8
keywords:
- WDK GDL の構成ディレクティブのディレクティブ
- ソース ファイル WDK GDL の構成ディレクティブ
- WDK GDL の構成ディレクティブ
- パーサー WDK GDL、ディレクティブ
- 機能ディレクティブ WDK GDL
- Option ディレクティブ WDK GDL
- Switch Case/ディレクティブ WDK GDL
- 既定の WDK GDL ディレクティブ
- DefaultOption ディレクティブ WDK GDL
- 制約ディレクティブ WDK GDL
- InvalidCombinations ディレクティブ WDK GDL
- WDK GDL、ディレクティブの構成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 950f183fcbeb5e4d28c69068c856dd6748372649
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574368"
---
# <a name="gdl-directives-for-configurations"></a>構成の GDL ディレクティブ


GDL には、構成の定義および操作するディレクティブがあります。

GDL には、次の構成ディレクティブが含まれています。

-   **\*機能**機能に関連する構成パラメーターを定義します。

-   **\*オプション**各構成パラメーターに割り当てることが許可されている状態のセットを定義します。 これらの状態を許可されていると呼ばれます*オプション*します。

-   **\*スイッチ**、 **\*ケース**、および**既定**指定した構成パラメーターへの依存関係を確立します。

-   **\*DefaultOption**既定の構成を構築します。

-   **\*制約**と **\*InvalidCombinations**無効な構成を指定します。 これらのディレクティブが発生した場合、GDL パーサーは有効な (または制約のない) 構成を作成するように変更しようとします。

構成ディレクティブの詳細については、[GDL 構成](gdl-configurations.md)を参照してください。

 

 




