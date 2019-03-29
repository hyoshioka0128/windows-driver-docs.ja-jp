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
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579991"
---
# <a name="making-driver-code-or-data-pageable"></a>ドライバーのコードまたはデータをページング可能にする





ドライバーのルーチンをページングするためには、IRQL でが実行されることを確認してください&lt;ディスパッチ\_スピン ロックのレベルと、それを取得しませんいずれか。

このセクションでは、次のトピックについて説明します。

[ページング可能な可能性のあるコードを検出します。](detecting-code-that-can-be-pageable.md)

[ページング可能なコードの分離](isolating-pageable-code.md)

[ロックのページング可能なコードやデータ](locking-pageable-code-or-data.md)

[全体のドライバーのページング](paging-an-entire-driver.md)

 

 




