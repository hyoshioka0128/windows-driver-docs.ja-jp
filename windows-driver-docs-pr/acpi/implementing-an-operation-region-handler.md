---
title: 操作領域ハンドラーを実装する
description: 操作領域ハンドラーを実装する
ms.assetid: e435393c-d637-45c1-ab65-0b23f796ec02
keywords:
- ACPI デバイス WDK、操作リージョン
- 操作リージョン WDK ACPI
- 関数ドライバー WDK ACPI、操作リージョン
- WDM 関数ドライバー WDK ACPI、操作リージョン
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49ad55b0afb9ef41fc4b7126e5744d915af21e80
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827002"
---
# <a name="implementing-an-operation-region-handler"></a>操作領域ハンドラーを実装する





ドライバーは、操作領域ハンドラーを提供する必要があります。このハンドラーは、 [**Pacpi\_OP\_region\_ハンドラー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/oprghdlr/nc-oprghdlr-acpi_op_region_handler)で型指定されたコールバックです。 ACPI ドライバーは、操作ハンドラーを呼び出して、ドライバーの操作領域のデータフィールドにアクセスします。 関数ドライバーと ACPI BIOS の組み合わせ操作は、ベンダーによって定義され、デバイスに固有です。 一般に、関数ドライバーと ACPI BIOS は、操作領域内のインデックスにアクセスします。これにより、デバイス固有の操作が行われ、すべての情報が適切に返されます。

通常、操作領域ハンドラーは、ACPI ドライバーがハンドラーに渡す次のパラメーターを使用します。

-   *AccessType*アクセスが読み取りと書き込みのどちらであるかを指定します。

    アクセスが読み取りの場合、データは操作領域のメモリバッファーから*データ*バッファーに転送されます。 アクセスが書き込みの場合、データは*データ*バッファーから操作領域のメモリバッファーに転送されます。 「[操作領域へのアクセス](accessing-an-operation-region.md)」を参照してください。

-   *アドレス*操作領域のメモリバッファー内のバイトオフセットを指定します。

-   *Size*転送するバイト数を指定します。

-   *Data*転送用の ACPI ドライバーによって提供されるバッファーを指定します。

-   *コンテキスト*は、操作領域ハンドラーに対してドライバーが登録した操作領域のコンテキストを指定します。

    操作領域コンテキストは関数ドライバーによってのみ使用され、デバイス固有です。

前述のパラメーターに加えて、ACPI ドライバーは、操作領域のハンドラーポインター (操作領域オブジェクト、完了ハンドラー、および完了コンテキスト) にも渡します。 ただし、関数ドライバーはハンドラーで操作領域オブジェクトを使用せず、完了ハンドラーとコンテキストは内部使用のために予約されています。

 

 




