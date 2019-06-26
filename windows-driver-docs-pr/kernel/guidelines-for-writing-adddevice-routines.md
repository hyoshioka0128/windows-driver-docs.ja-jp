---
title: AddDevice ルーチンの記述に関するガイドライン
description: AddDevice ルーチンの記述に関するガイドライン
ms.assetid: 8df36af5-158c-4c14-9fc2-2c3f997c2098
keywords:
- AddDevice ルーチン WDK カーネルのデザイン ガイドライン
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfb3d1fefa0247baf24e8be5dd2f7e14adf2b6bc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375233"
---
# <a name="guidelines-for-writing-adddevice-routines"></a>AddDevice ルーチンの記述に関するガイドライン





書き込み時に、次のデザイン ガイドラインを考慮して、 [ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)ルーチン。

-   フィルター ドライバーが判断した場合、 *AddDevice*ルーチンを呼び出したサービスに必要はありません、デバイスのフィルター ドライバーは、状態を返す必要があります\_成功した場合、デバイスに読み込まれるデバイス スタックの残りの部分を許可します。 フィルター ドライバーは、デバイス オブジェクトを作成したり、デバイス スタック; にアタッチありません。だけ、フィルター ドライバーは成功を返しますでき、スタックに追加するドライバーの残りの部分になります。

-   ドライバーでは、カーネル定義オブジェクトおよび executive のスピン ロックを使用して、デバイス オブジェクトのデバイスの拡張機能には、通常、記憶域を提供する必要があります。 ドライバーは、I/O マネージャーまたは他のシステム コンポーネントから取得した特定のオブジェクトへのポインターの記憶域を提供する必要があります。

    長期的な I/O バッファーまたはルック アサイド リストのなどのドライバーのニーズに合わせて、空きシステム メモリを割り当てることがあります。 そうである場合、 *AddDevice*ルーチンは、次のルーチンを呼び出すことができます。

    [**Exallocatepoolwithtag に**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithtag)ページまたは非ページ システム容量のメモリ

    [**ExInitializePagedLookasideList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinitializepagedlookasidelist)または[ **ExInitializeNPagedLookasideList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinitializenpagedlookasidelist)ページまたは非ページのルック アサイド リストの初期化

-   ドライバーは、デバイス専用のスレッドを持っているか、任意のカーネル定義のディスパッチャー オブジェクトで待機の場合、 *AddDevice*ルーチンが初期化[カーネルのディスパッチャー オブジェクト](kernel-dispatcher-objects.md)します。

-   ドライバー、executive スピン ロックを使用してまたは割り込みスピン ロックは記憶域の提供、 *AddDevice*ルーチンがこれらのスピン ロックを初期化します。 参照してください[スピン ロック](spin-locks.md)詳細についてはします。

-   呼び出すときに、開いているファイルのセキュリティを強化[ **IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatedevice)します。

    ファイルを指定\_デバイス\_SECURE\_への呼び出しで開いている特性**IoCreateDevice**します。 Windows NT 4.0 SP5 以降、このような特性はサポートされています。 開いているすべての要求のデバイス オブジェクトに対するセキュリティ チェックを実行する I/O マネージャーがよう指示します。 ベンダーへの呼び出しでこのような特性を指定する必要があります**IoCreateDevice**場合、ファイル\_デバイス\_SECURE\_INF またはデバイスの INF、デバイスのクラスのインストーラーで開いている特性が設定されていません。ドライバーが表示されますが、独自のセキュリティ チェックを行いません。 (詳細については、次を参照してください[デバイス Namespace のアクセスを制御する](controlling-device-namespace-access.md)。)。

    ドライバー ファイルを設定する場合\_デバイス\_SECURE\_を呼び出すときに、開いている特性**IoCreateDevice**、I/O マネージャーが、関連するオープンにデバイス オブジェクトのセキュリティ記述子を適用または末尾のファイル名が表示されます。 たとえば場合、ファイル\_デバイス\_SECURE\_オープンに設定されて\\デバイス\\foo, 場合に\\デバイス\\foo のみ開くことによって、管理者、 \\デバイス\\foo\\abc が管理者によって開くこともできます。 I/O マネージャー、ただし、通常のユーザーが開けないように\\デバイス\\foo および\\デバイス\\foo\\abc です。

    デバイスの 1 つのドライバーでは、このような特性を設定、PnP マネージャーにより、デバイスのすべてのデバイス オブジェクトに伝達します。

 

 




