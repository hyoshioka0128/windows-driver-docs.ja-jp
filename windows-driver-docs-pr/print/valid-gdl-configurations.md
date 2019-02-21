---
title: 有効な GDL 構成
description: 有効な GDL 構成
ms.assetid: 68dbe7f7-4f6d-46e5-b2f1-27b123c4bedb
keywords:
- GDL WDK の構成
- パーサーの構成を検証、WDK GDL
- WDK GDL、有効な構成の構成
- GDL WDK の構成を検証
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 001d71ea7dd73e6303894488457410d8a66259ed
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549409"
---
# <a name="valid-gdl-configurations"></a>有効な GDL 構成


GDL パーサー インターフェイス関数では、パーサーでクライアントの設定を間違えたと無効な構成を備えた可能性がある場合がありますので、受信の構成は常に検証します。 無効な構成の詳細については、次を参照してください。 [GDL の無効な設定を使用して](using-invalid-gdl-configurations.md)します。

有効な構成では、次の条件を満たします。

-   構成には、GDL で定義されている各パラメーターのエントリが含まれています。

-   構成に、GDL で定義されていないパラメーターのエントリが含まれていません。

-   各パラメーターに割り当てられている値によって定義されます、\*そのパラメーターのオプションの構成体です。

-   PICKONE パラメーターには、割り当てられている 1 つだけの値があります。

-   PICKMANY パラメーターには、割り当てられている少なくとも 1 つの値があります。

パーサーの検証プロセスのための構成の目的の損失を防ぐため、パーサー関数に有効な構成を渡す必要があります。

 

 




