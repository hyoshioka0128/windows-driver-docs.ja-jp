---
title: IPrintCoreHelperPS インターフェイスの詳細
description: IPrintCoreHelperPS インターフェイスの詳細
ms.assetid: 0e00012c-6ced-4369-b367-675465e29d93
keywords:
- IPrintCoreHelperPS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18b4bea3e7f34b7fd840b7b81e675f0a692d8af5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382059"
---
# <a name="details-of-the-iprintcorehelperps-interface"></a>IPrintCoreHelperPS インターフェイスの詳細


GDL パーサーに相当する型を持たない Pscript5 PPD ファイルに表示されるデータを読み取る Pscript5 ドライバーでは、追加のメソッドが提供されているためです。 すべてのベースのメソッドだけでなく**IPrintCoreHelper** 、インターフェイス、 **IPrintCoreHelperPS**インターフェイスには PPD ファイル内のデータへのアクセスを提供する次のメソッドが含まれています。

-   [**IPrintCoreHelperPS::GetFeatureAttribute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcorehelperps-getfeatureattribute)

-   [**IPrintCoreHelperPS::GetGlobalAttribute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcorehelperps-getglobalattribute)

-   [**IPrintCoreHelperPS::GetOptionAttribute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcorehelperps-getoptionattribute)

PPD 情報は、構成に依存しない、ためには、入力を指定する必要はありません[ **DEVMODEW** ](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)これらのメソッドのパラメーター。

 

 




