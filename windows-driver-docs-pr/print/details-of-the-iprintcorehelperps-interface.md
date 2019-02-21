---
title: IPrintCoreHelperPS インターフェイスの詳細
description: IPrintCoreHelperPS インターフェイスの詳細
ms.assetid: 0e00012c-6ced-4369-b367-675465e29d93
keywords:
- IPrintCoreHelperPS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a89d865c49e23ed8645a572342476606a17c1bed
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558362"
---
# <a name="details-of-the-iprintcorehelperps-interface"></a>IPrintCoreHelperPS インターフェイスの詳細


GDL パーサーに相当する型を持たない Pscript5 PPD ファイルに表示されるデータを読み取る Pscript5 ドライバーでは、追加のメソッドが提供されているためです。 すべてのベースのメソッドだけでなく**IPrintCoreHelper** 、インターフェイス、 **IPrintCoreHelperPS**インターフェイスには PPD ファイル内のデータへのアクセスを提供する次のメソッドが含まれています。

-   [**IPrintCoreHelperPS::GetFeatureAttribute**](https://msdn.microsoft.com/library/windows/hardware/ff551998)

-   [**IPrintCoreHelperPS::GetGlobalAttribute**](https://msdn.microsoft.com/library/windows/hardware/ff552899)

-   [**IPrintCoreHelperPS::GetOptionAttribute**](https://msdn.microsoft.com/library/windows/hardware/ff552903)

PPD 情報は、構成に依存しない、ためには、入力を指定する必要はありません[ **DEVMODEW** ](https://msdn.microsoft.com/library/windows/hardware/ff552837)これらのメソッドのパラメーター。

 

 




