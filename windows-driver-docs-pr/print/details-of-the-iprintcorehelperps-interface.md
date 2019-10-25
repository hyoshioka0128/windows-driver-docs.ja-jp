---
title: IPrintCoreHelperPS インターフェイスの詳細
description: IPrintCoreHelperPS インターフェイスの詳細
ms.assetid: 0e00012c-6ced-4369-b367-675465e29d93
keywords:
- Iprintcoreの Perps
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 708a6c67a7da234d786cd7379df7569d9ddcabeb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829018"
---
# <a name="details-of-the-iprintcorehelperps-interface"></a>IPrintCoreHelperPS インターフェイスの詳細


Pscript5 は GDL パーサーに相当するものではないため、Pscript5 ドライバーでは、PPD ファイルに表示されるデータを読み取るための追加のメソッドが提供されています。 **Iprintcorehelper**ヘルパーインターフェイスには、基本の**iprintcorehelper**インターフェイスのすべてのメソッドに加えて、次のメソッドが含まれています。これらのメソッドは、PPD ファイル内のデータへのアクセスを提供します。

-   [**Iprintcore/Perps:: GetFeatureAttribute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcorehelperps-getfeatureattribute)

-   [**Iprintcore/Perps:: GetGlobalAttribute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcorehelperps-getglobalattribute)

-   [**IprintcoreGetOptionAttribute Perps::** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcorehelperps-getoptionattribute)

PPD 情報は構成に依存しないため、これらのメソッドに[**Devmodew**](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)パラメーターを指定する必要はありません。

 

 




