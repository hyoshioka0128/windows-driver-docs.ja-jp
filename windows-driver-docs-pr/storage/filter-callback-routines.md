---
title: フィルター コールバック ルーチン
description: フィルター コールバック ルーチン
ms.assetid: 3d9f874c-f026-40fc-a97d-0d4cefa3d1f9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a57929b22e8bd58bd6abb01405af1b400b2e9a21
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356000"
---
# <a name="filter-callback-routines"></a>フィルター コールバック ルーチン


クラッシュ ダンプのドライバーでは、クラッシュ ダンプ フィルター ドライバーでは、次のコールバック ルーチンをサポートしています。 これらのコールバック ルーチンは必須ではないため、クラッシュ ダンプ フィルター ドライバーは、自由にのみ、目的の機能を追加するために必要なコールバック ルーチンを実装できます。

[**ダンプ\_開始**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntdddump/nc-ntdddump-dump_start)

[**ダンプ\_書き込み**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntdddump/nc-ntdddump-dump_write)

[**ダンプ\_読み取り**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntdddump/nc-ntdddump-dump_read)

[**ダンプ\_完了**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntdddump/nc-ntdddump-dump_finish)

[**ダンプ\_アンロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntdddump/nc-ntdddump-dump_unload)

 

 




