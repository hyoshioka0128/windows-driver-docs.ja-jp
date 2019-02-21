---
title: 操作の領域へのアクセス
description: 操作の領域へのアクセス
ms.assetid: 9a1aa29e-679c-4f7f-a16c-3e1c94be66a7
keywords:
- ACPI デバイス WDK、領域の操作
- 操作のリージョン WDK ACPI
- 機能ドライバー WDK ACPI、領域の操作
- WDM 関数ドライバー WDK ACPI、領域の操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a8bb43106093c91786fbbb8999fe3fc809d6f5e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553379"
---
# <a name="accessing-an-operation-region"></a>操作の領域へのアクセス





関数ドライバー操作のリージョン ハンドラーを登録する場合、ドライバーが ACPI アクセスの種類を指定する必要があります\_OPREGION\_アクセス\_AS\_COOKED します。 加工済みのデバイスに関数ドライバーからではなく、デバイスの機能のドライバーを ACPI デバイスから情報のアクセスをサポート転送します。

システム提供の ACPI ドライバーだけでは、操作、リージョン内のデータを変更します。 関数のドライバーでは、操作、リージョン内のデータを読み取ることができます。 ただし、データは変更する必要があります。 呼び出されると、操作のリージョン ハンドラーは操作の領域と ACPI ドライバーのデータ バッファーの間を転送します。 ACPI ドライバーでは、操作の領域でデータ フィールドを読み書きする正しいバイトへのアクセスを管理します。

 

 




