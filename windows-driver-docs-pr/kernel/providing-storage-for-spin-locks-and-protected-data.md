---
title: スピン ロックおよび保護されたデータ用の記憶域の提供
description: スピン ロックおよび保護されたデータ用の記憶域の提供
ms.assetid: bde18474-10c3-4d9a-b120-6cbd5fc675cc
keywords:
- storage WDK スピンロック
- スピンロックで保護されたデータの格納
- スピンロック WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b0b4a837bcaf50a2256c278b468ac35a288f8263
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838481"
---
# <a name="providing-storage-for-spin-locks-and-protected-data"></a>スピン ロックおよび保護されたデータ用の記憶域の提供





デバイスの起動時に、ドライバーは、次のいずれかの場所にあるスピンロックで保護されたデータまたはリソース、および対応するスピンロックに対して常駐ストレージを割り当てる必要があります。

-   ドライバーが IoCreateDevice を呼び出すことによって設定するデバイスオブジェクトのデバイス拡張機能[](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)

-   ドライバーが IoCreateController を呼び出すことによって設定するコントローラーオブジェクトのコントローラー拡張機能[](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatecontroller)

-   [ **Exallocatepoolwithtag**を呼び出すことによってドライバーが取得する、ページングされていないシステム領域のメモリ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)

スピンロックを保持しながら、ページング可能なデータにアクセスしようとすると、そのページが存在しない場合に致命的なページフォールトが発生します。 無効なスピンロック (ページング可能なメモリに格納され、現在はページアウトされているため) を参照すると、致命的なページフォールトが発生します。

ドライバーは、使用する可能性がある次の種類のエグゼクティブスピンロックのそれぞれに対して記憶域を提供する必要があります。

- ドライバーが明示的に取得し、いずれかの**Ke * Xxx*** スピンロックルーチンを使用して解放するスピンロック。

- すべてのスピンロックは、任意の**Exinterlocked ロック * Xxx*** ルーチンのパラメーターとして使用されます。

ドライバーは、ISR または[*SynchCritSection*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine)ルーチンから**Exinterlocked ロック * xxx*** ルーチンを呼び出すことができますが、 **Ke * xxx*** ルーチンを使用して、ディスパッチ\_レベルより大きい IRQL でスピンロックを取得したり解放したりすることはできません。 その結果、 **Ke*Xxx*スピンロック**と**exinterlocked ロック * Xxx*** ルーチンの呼び出しの間でスピンロックを再利用するすべてのドライバーは、IRQL &lt;= DISPATCH\_レベルで実行中にすべての呼び出しを行う必要があります。

ドライバーは、2つのルーチンが同じ IRQL でスピンロックを使用している限り、別の Exinterlocked ロックされた *** Xxx*** ルーチンと同じスピンロックを**ExInterlockedInsertHeadList**に渡すことができます。 スピンロックの使用によるパフォーマンスへの影響の詳細については、「[スピンロックの使用: 例](using-spin-locks--an-example.md)」を参照してください。

デバイスドライバーでは、executive スピンロックのストレージに加えて、multivector ISR または複数の ISR がある場合に、その割り込みオブジェクトに関連付けられる別のスピンロックのストレージを提供する必要があります。

 

 




