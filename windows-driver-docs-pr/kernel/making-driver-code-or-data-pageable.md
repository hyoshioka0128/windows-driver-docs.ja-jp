---
title: ドライバーのコードまたはデータをページング可能にする
description: ドライバーのコードまたはデータをページング可能にする
ms.assetid: c4ffd222-8ea5-48df-9c79-7d68e5462b3e
keywords:
- メモリ管理の WDK カーネル、ページング可能なドライバー
- ページング可能なドライバー WDK カーネルを設定します。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81f03445b66b962193a64deb4e7522c884f05ea2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378738"
---
# <a name="making-driver-code-or-data-pageable"></a>ドライバーのコードまたはデータをページング可能にする





ドライバーのルーチンをページングするためには、IRQL でが実行されることを確認してください&lt;ディスパッチ\_スピン ロックのレベルと、それを取得しませんいずれか。

このセクションでは、次のトピックについて説明します。

[ページング可能な可能性のあるコードを検出します。](detecting-code-that-can-be-pageable.md)

[ページング可能なコードの分離](isolating-pageable-code.md)

[ロックのページング可能なコードやデータ](locking-pageable-code-or-data.md)

[全体のドライバーのページング](paging-an-entire-driver.md)

 

 




