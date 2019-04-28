---
title: AVStream のデバイス ミューテックス
description: AVStream のデバイス ミューテックス
ms.assetid: cec2a040-59d6-44ef-aef1-04f434811d60
keywords:
- AVStream mutexes WDK
- ミュー テックス WDK AVStream
- デバイスのミュー テックス WDK AVStream
- WDK AVStream の同期
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 076849ef6bfbb21aafd6be5f60750e6ff57f1139
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374052"
---
# <a name="device-mutex-in-avstream"></a>AVStream のデバイス ミューテックス





フィルターまで、デバイスから階層内のオブジェクトを同期するのにには、デバイスのミュー テックスを使用します。 各 AVStream デバイスでは、1 つの関連付けられているデバイスのミュー テックスを持っています。 両方の作成と破棄は、ファクトリをフィルター処理して、フィルターは、このミュー テックスと同期されます。 特定のプラグ アンド プレイと電源管理操作は、このミュー テックスとも同期されます。 ミニドライバーは、デバイスのミュー テックスに関して 2 つの主な問題について説明します。

オブジェクト階層の安定したことが保証されて*のみ*デバイス ミュー テックスが保持されている場合、個別のフィルターまで、デバイスから。 結果として、ミニドライバーは、手動で呼び出すことによってフィルター ファクトリを作成する前のデバイスのミュー テックスを取得する必要があります[ **KsCreateFilterFactory**](https://msdn.microsoft.com/library/windows/hardware/ff561650)します。 ミニドライバーを呼び出して、オブジェクト階層を移動する前に、デバイスのミュー テックスを取得する必要がありますも、**Ks***Xxx***GetFirstChild * * * Xxx*と **Ks***Xxx***GetNextSibling * * * Xxx*関数。

AVStream は、次の要求を受信すると、ミニドライバーに代わってデバイス ミュー テックスを保持します。

-   [**IRP\_MN\_クエリ\_停止\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551725)

-   [**IRP\_MN\_クエリ\_削除\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551705)

-   [*PostStart ディスパッチ*](https://msdn.microsoft.com/library/windows/hardware/ff554284)

-   [**IRP\_MN\_START\_DEVICE**](https://msdn.microsoft.com/library/windows/hardware/ff551749)

-   [**IRP\_MN\_クエリ\_電源**](https://msdn.microsoft.com/library/windows/hardware/ff551699)

-   [**IRP\_MN\_SET\_POWER**](https://msdn.microsoft.com/library/windows/hardware/ff551744)

-   スリープし、復帰のフィルターと pin で通知します。 参照してください[ **KsFilterRegisterPowerCallbacks** ](https://msdn.microsoft.com/library/windows/hardware/ff562550)と[ **KsPinRegisterPowerCallbacks**](https://msdn.microsoft.com/library/windows/hardware/ff563525)します。

再帰的にことはできませんデバイス ミュー テックスを取得することに注意してください。 次の例を検討してください。 AVStream は、スリープという通知を受け取ります。 前述のよう、ミニドライバーに代わって、デバイスのミュー テックスがかかります。 AVStream し、スレッド A のコンテキストで、ミニドライバーで提供されるコールバック ルーチンを呼び出すと場合、ミニドライバー後しようとしないでスレッド自体でデッドロックが発生するスレッド A A. の実行とデバイスのミュー テックスを取得します。

デバイスのミュー テックスが既に保持されている間、AVStream は多くの場合、フィルター コントロール ミュー テックスを取得します。 その結果、一般的な規則として、スレッド フィルター コントロール ミュー テックスが実行した後で受け取ることはできませんデバイス ミュー テックス。

デバイスのミュー テックスを操作するには、次の関数を使用します。

[**KsAcquireDevice**](https://msdn.microsoft.com/library/windows/hardware/ff560911)、 [ **KsReleaseDevice**](https://msdn.microsoft.com/library/windows/hardware/ff566783)

 

 




