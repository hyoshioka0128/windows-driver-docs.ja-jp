---
title: AVStream のミューテックス
description: AVStream のミューテックス
ms.assetid: 011edaaa-7449-41c3-8cfb-0d319901af8b
keywords:
- AVStream mutexes WDK
- ミュー テックス WDK AVStream
- WDK AVStream オブジェクト
- WDK AVStream の階層
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65dda3311d6ffbc40dedd06e6d1b396e1b79cde5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329934"
---
# <a name="mutexes-in-avstream"></a>AVStream のミューテックス





AVStream ミニドライバーは、ミュー テックスとプロセスの制御ゲートを使用して、オブジェクトへのアクセスを同期します。 プロセス制御ゲートの詳細については、次を参照してください。 [AVStream でのフロー制御ゲート](flow-control-gates-in-avstream.md)します。

AVStream は、ミニドライバーに直接アクセスすることで、すべての 3 つミュー テックスの異なるがあります。

[AVStream でデバイスのミュー テックス](device-mutex-in-avstream.md)

[AVStream でコントロールのミュー テックスをフィルター処理します。](filter-control-mutex-in-avstream.md)

[AVStream でミュー テックスの処理](processing-mutex-in-avstream.md)

フィルター処理するのにデバイスからの階層オブジェクトを同期するのにには、デバイスのミュー テックスを使用します。 ピン留めするのにフィルターからオブジェクトを同期するのにには、フィルター コントロール ミュー テックスを使用します。

いくつかの AVStream API 関数では、その特定のミュー テックスを保持する必要があります。 関連する関数の参照ページ状態場合、その特定の関数を呼び出すときに、特定のミュー テックスを保持する必要があります。

 

 




