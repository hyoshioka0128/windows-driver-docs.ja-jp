---
title: 標準の WMI のブロックをサポートしています。
description: 標準の WMI のブロックをサポートしています。
ms.assetid: ddec3afb-8274-4eff-93ef-b0a07fd7c13a
keywords:
- WMI の WDK カーネルでは、イベント ブロック
- イベントは、WDK の WMI をブロックします。
- WDK の WMI のデータ ブロックします。
- WMI の WDK カーネルでは、データのブロック
- WDK の WMI をブロックします。
- 標準ブロック WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee18351c104f7d79c262528f9153d066004d663d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539119"
---
# <a name="supporting-standard-wmi-blocks"></a>標準の WMI のブロックをサポートしています。





各ドライバーは、いずれかをサポートする必要があります*標準ブロック*その型のドライバーに対して定義されています。 標準ブロックは、仕入先に関係なく、指定された型のすべてのデバイスに対して一貫性のあるデータを WMI クライアントを提供します。

標準のブロック、ドライバーをサポートするには。

-   WMI を使用すると、その他の」の説明に従って、ドライバーによってサポートされている任意の標準とカスタム要素、ブロックを登録します[WMI データ プロバイダーとして登録する](registering-as-a-wmi-data-provider.md)します。

-   ドライバーのデバイス オブジェクトのポインターを指定するすべての WMI 要求を処理**Parameters.WMI.ProviderId**とでは、標準的なブロックの GUID **Parameters.WMI.DataPath** 」の説明に従って、[WMI 要求を処理して](handling-wmi-requests.md)します。

標準ブロック用の MOF クラスは、システム提供の MOF ファイルに発行されます。 ドライバーには、WMI データベース内のブロックが重複するがあるために、独自の MOF ファイル内の標準的なブロックが再定義しない必要があります。

現時点では、標準のブロックのクラス定義は、Windows Driver Kit (WDK) で含まれているファイル wmicore.mof に発行されます。

 

 




