---
title: 操作領域のメモリ バッファーを維持する
description: 操作領域のメモリ バッファーを維持する
ms.assetid: 4abe82ec-d8c4-43c1-a72f-5114ba07160e
keywords:
- ACPI デバイス WDK、領域の操作
- 操作のリージョン WDK ACPI
- 機能ドライバー WDK ACPI、領域の操作
- WDM 関数ドライバー WDK ACPI、領域の操作
- 操作の領域のメモリ バッファー WDK ACPI
- メモリ バッファーの WDK ACPI
ms.date: 01/24/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6b8abd68c6a0e1d10f05d3f996348b799da1e3ee
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582284"
---
# <a name="maintaining-an-operation-region-memory-buffer"></a>操作領域のメモリ バッファーを維持する



ドライバーは、操作の領域のメモリ バッファーを保持します。 メモリ バッファーには、操作を地域に関連付けられているデータ フィールドが含まれています。 ACPI ドライバーでは、操作の領域のメモリ バッファー内のデータ フィールドにアクセスする操作領域ハンドラーを呼び出します。

操作の領域のメモリ バッファーは、次のように従う必要があります。

-   非ページ システム メモリからメモリ バッファーを割り当てる必要があります。

-   バッファー サイズは、ACPI デバイスに対して定義されている操作の領域のサイズ以上である必要があります。

-   バッファーは、ドライバーは、それにアクセスする操作領域ハンドラーを登録する前に割り当てられているし、ハンドラーが登録されている限り、保持する必要があります。

操作の領域の制約に関する詳細については、、 [Advanced Configuration and Power Interface Specification](https://go.microsoft.com/fwlink/p/?linkid=866846)を参照してください。

 

 



