---
title: AddDevice ルーチンの記述に関するガイドライン
description: AddDevice ルーチンの記述に関するガイドライン
ms.assetid: 8df36af5-158c-4c14-9fc2-2c3f997c2098
keywords:
- AddDevice ルーチン WDK カーネルのデザイン ガイドライン
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d39a6ff5b8adc357c4e788b336131b2ff3a682d7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359904"
---
# <a name="guidelines-for-writing-adddevice-routines"></a>AddDevice ルーチンの記述に関するガイドライン





書き込み時に、次のデザイン ガイドラインを考慮して、 [ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)ルーチン。

-   フィルター ドライバーが判断した場合、 *AddDevice*ルーチンを呼び出したサービスに必要はありません、デバイスのフィルター ドライバーは、状態を返す必要があります\_成功した場合、デバイスに読み込まれるデバイス スタックの残りの部分を許可します。 フィルター ドライバーは、デバイス オブジェクトを作成したり、デバイス スタック; にアタッチありません。だけ、フィルター ドライバーは成功を返しますでき、スタックに追加するドライバーの残りの部分になります。

-   ドライバーでは、カーネル定義オブジェクトおよび executive のスピン ロックを使用して、デバイス オブジェクトのデバイスの拡張機能には、通常、記憶域を提供する必要があります。 ドライバーは、I/O マネージャーまたは他のシステム コンポーネントから取得した特定のオブジェクトへのポインターの記憶域を提供する必要があります。

    長期的な I/O バッファーまたはルック アサイド リストのなどのドライバーのニーズに合わせて、空きシステム メモリを割り当てることがあります。 そうである場合、 *AddDevice*ルーチンは、次のルーチンを呼び出すことができます。

    [**Exallocatepoolwithtag に**](https://msdn.microsoft.com/library/windows/hardware/ff544520)ページまたは非ページ システム容量のメモリ

    [**ExInitializePagedLookasideList** ](https://msdn.microsoft.com/library/windows/hardware/ff545309)または[ **ExInitializeNPagedLookasideList** ](https://msdn.microsoft.com/library/windows/hardware/ff545301)ページまたは非ページのルック アサイド リストの初期化

-   ドライバーは、デバイス専用のスレッドを持っているか、任意のカーネル定義のディスパッチャー オブジェクトで待機の場合、 *AddDevice*ルーチンが初期化[カーネルのディスパッチャー オブジェクト](kernel-dispatcher-objects.md)します。

-   ドライバー、executive スピン ロックを使用してまたは割り込みスピン ロックは記憶域の提供、 *AddDevice*ルーチンがこれらのスピン ロックを初期化します。 参照してください[スピン ロック](spin-locks.md)詳細についてはします。

-   呼び出すときに、開いているファイルのセキュリティを強化[ **IoCreateDevice**](https://msdn.microsoft.com/library/windows/hardware/ff548397)します。

    ファイルを指定\_デバイス\_SECURE\_への呼び出しで開いている特性**IoCreateDevice**します。 Windows NT 4.0 SP5 以降、このような特性はサポートされています。 開いているすべての要求のデバイス オブジェクトに対するセキュリティ チェックを実行する I/O マネージャーがよう指示します。 ベンダーへの呼び出しでこのような特性を指定する必要があります**IoCreateDevice**場合、ファイル\_デバイス\_SECURE\_INF またはデバイスの INF、デバイスのクラスのインストーラーで開いている特性が設定されていません。ドライバーが表示されますが、独自のセキュリティ チェックを行いません。 (詳細については、次を参照してください[デバイス Namespace のアクセスを制御する](controlling-device-namespace-access.md)。)。

    ドライバー ファイルを設定する場合\_デバイス\_SECURE\_を呼び出すときに、開いている特性**IoCreateDevice**、I/O マネージャーが、関連するオープンにデバイス オブジェクトのセキュリティ記述子を適用または末尾のファイル名が表示されます。 たとえば場合、ファイル\_デバイス\_SECURE\_オープンに設定されて\\デバイス\\foo, 場合に\\デバイス\\foo のみ開くことによって、管理者、 \\デバイス\\foo\\abc が管理者によって開くこともできます。 I/O マネージャー、ただし、通常のユーザーが開けないように\\デバイス\\foo および\\デバイス\\foo\\abc です。

    デバイスの 1 つのドライバーでは、このような特性を設定、PnP マネージャーにより、デバイスのすべてのデバイス オブジェクトに伝達します。

 

 




