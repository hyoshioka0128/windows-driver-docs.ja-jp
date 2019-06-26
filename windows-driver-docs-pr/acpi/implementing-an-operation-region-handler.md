---
title: 操作領域ハンドラーを実装する
description: 操作領域ハンドラーを実装する
ms.assetid: e435393c-d637-45c1-ab65-0b23f796ec02
keywords:
- ACPI デバイス WDK、領域の操作
- 操作のリージョン WDK ACPI
- 機能ドライバー WDK ACPI、領域の操作
- WDM 関数ドライバー WDK ACPI、領域の操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b33bf2f8820507cd9b8409532f6444b7a30c65c8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355837"
---
# <a name="implementing-an-operation-region-handler"></a>操作領域ハンドラーを実装する





ドライバーは、これは操作リージョン ハンドラーを提供する必要があります、 [ **PACPI\_OP\_リージョン\_ハンドラー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/oprghdlr/nc-oprghdlr-acpi_op_region_handler)-コールバックの型を指定します。 ACPI ドライバーでは、ドライバーの操作のリージョン内のデータ フィールドにアクセスする操作のハンドラーを呼び出します。 関数ドライバーと ACPI BIOS の結合操作は、ベンダー定義し、デバイスに固有です。 一般に、関数のドライバーと ACPI BIOS は、デバイス固有の操作が発生し、戻り値のすべての情報が適切なインデックス操作の領域でアクセスします。

操作リージョン ハンドラーは、通常、ACPI ドライバーは、ハンドラーに渡される次のパラメーターを使用します。

-   *AccessType*アクセスが読み取りまたは書き込みがあるかどうかを指定します。

    操作リージョン メモリ バッファーからデータを転送へのアクセスが読み取りの場合、*データ*バッファー。 データを転送へのアクセスが書き込みの場合、*データ*バッファーを操作の領域のメモリ バッファー。 参照してください[、操作の領域へのアクセス](accessing-an-operation-region.md)します。

-   *アドレス*操作領域のメモリ バッファーのバイト オフセットを指定します。

-   *サイズ*を転送するバイト数を指定します。

-   *データ*ACPI ドライバーによってデータ転送の指定されたバッファーを指定します。

-   *コンテキスト*操作リージョン ハンドラーのドライバーが登録されている操作地域のコンテキストを指定します。

    操作の地域のコンテキストは、関数のドライバーでのみ使用、デバイスに固有です。

上記のパラメーターに加え、ACPI ドライバーも渡します。、次の操作リージョン ハンドラ ポインター: 操作の領域オブジェクト、完了ハンドラー、および完了コンテキスト。 ただし、関数ドライバーがハンドラーで、操作の領域オブジェクトを使用していないし、完了ハンドラーとコンテキストは内部使用のため予約されています。

 

 




