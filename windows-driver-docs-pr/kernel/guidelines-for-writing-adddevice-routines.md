---
title: AddDevice ルーチンの記述に関するガイドライン
description: AddDevice ルーチンの記述に関するガイドライン
ms.assetid: 8df36af5-158c-4c14-9fc2-2c3f997c2098
keywords:
- AddDevice ルーチン WDK カーネル、設計ガイドライン
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4855f91fa9d39a168a4686a58cef2e860b93df82
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838683"
---
# <a name="guidelines-for-writing-adddevice-routines"></a>AddDevice ルーチンの記述に関するガイドライン





[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンを記述するときは、次の設計ガイドラインを考慮してください。

-   フィルタードライバーによって、 *AddDevice*ルーチンがデバイスに対して呼び出されたと判断された場合、サービスを実行する必要はありません。フィルタードライバーは、デバイスの残りのデバイススタックを読み込むことができるように、状態\_SUCCESS を返す必要があります。 フィルタードライバーは、デバイスオブジェクトを作成したり、デバイススタックにアタッチしたりすることはありません。フィルタードライバーは、成功だけを返し、残りのドライバーをスタックに追加できるようにします。

-   ドライバーは、使用するカーネル定義オブジェクトと executive スピンロックに対して、通常、デバイスオブジェクトのデバイス拡張機能に記憶装置を提供する必要があります。 また、ドライバーは、i/o マネージャーまたはその他のシステムコンポーネントから取得した特定のオブジェクトへのポインターのストレージを提供する必要があります。

    長期間の i/o バッファーやルックアサイドリストなどのために、ドライバーのニーズに合わせて追加のシステム領域メモリを割り当てることができます。 その場合、 *AddDevice*ルーチンは次のルーチンを呼び出すことができます。

    ページングされたシステム領域または非ページシステム領域のメモリの[**Exallocatepoolwithtag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)

    [**ExInitializePagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializepagedlookasidelist)または[**ExInitializeNPagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializenpagedlookasidelist)は、ページングまたは非ページのルックアサイドリストを初期化します

-   ドライバーにデバイス専用のスレッドがある場合、またはカーネル定義のディスパッチャーオブジェクトを待機している場合は、 *AddDevice*ルーチンによって[カーネルディスパッチャーオブジェクト](kernel-dispatcher-objects.md)が初期化されることがあります。

-   ドライバーが executive スピンロックを使用するか、割り込みスピンロックのストレージを提供する場合、 *AddDevice*ルーチンはこれらのスピンロックを初期化することがあります。 詳細については、「[スピンロック](spin-locks.md)」を参照してください。

-   [**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)を呼び出すときに、ファイルオープンセキュリティを強化します。

    **IoCreateDevice**の呼び出しで、ファイル\_デバイス\_安全\_オープン特性を指定します。 この特性は、Windows NT 4.0 SP5 以降でサポートされています。 I/o マネージャーは、すべての開いている要求について、デバイスオブジェクトに対してセキュリティチェックを実行するように指示します。 ファイル\_デバイス\_セキュリティで保護された\_オープン特性がデバイスのクラスインストーラーの INF またはデバイスの INF で設定されておらず、ドライバーが独自のものを実行しない場合、ベンダーは**IoCreateDevice**の呼び出しでこの特性を指定する必要があります。セキュリティチェックが開きます。 (詳細については、「[デバイス名前空間へのアクセスの制御](controlling-device-namespace-access.md)」を参照してください)。

    ドライバーが**IoCreateDevice**を呼び出すときに、ファイル\_デバイス\_保護された\_オープン特性を設定した場合、i/o マネージャーは、デバイスオブジェクトのセキュリティ記述子を任意の相対オープンまたは末尾の filename ファイルに適用します。 たとえば、ファイル\_デバイス\_セキュア\_OPEN が \\デバイス\\foo に対して設定されている場合、\\Device\\foo を管理者のみが開くことができる場合は \\デバイス\\foo\\abc は、管理者が開くこともできます。 ただし、i/o マネージャーは、通常のユーザーが \\デバイス\\foo および \\デバイス\\foo\\abc を開けないようにします。

    デバイス用の1つのドライバーがこの特性を設定すると、PnP マネージャーはデバイスのすべてのデバイスオブジェクトにこの特性を伝達します。

 

 




