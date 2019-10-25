---
title: フィルター コールバック ルーチン
description: フィルター コールバック ルーチン
ms.assetid: 3d9f874c-f026-40fc-a97d-0d4cefa3d1f9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3552afba819c6a39e7905f4ffe833ab75bd61a4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844837"
---
# <a name="filter-callback-routines"></a>フィルター コールバック ルーチン


クラッシュダンプドライバーでは、クラッシュダンプフィルタードライバーの次のコールバックルーチンがサポートされています。 これらのコールバックルーチンは必須ではないため、クラッシュダンプフィルタードライバーは、必要な機能を追加するために必要なコールバックルーチンだけを実装することができます。

[**ダンプ\_開始**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdddump/nc-ntdddump-dump_start)

[**ダンプ\_書き込み**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdddump/nc-ntdddump-dump_write)

[**ダンプ\_読み取り**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdddump/nc-ntdddump-dump_read)

[**ダンプ\_完了**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdddump/nc-ntdddump-dump_finish)

[**ダンプ\_アンロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdddump/nc-ntdddump-dump_unload)

 

 




