---
title: スピン ロックおよび保護されたデータ用の記憶域の提供
description: スピン ロックおよび保護されたデータ用の記憶域の提供
ms.assetid: bde18474-10c3-4d9a-b120-6cbd5fc675cc
keywords:
- 記憶域 WDK スピン ロック
- スピン ロック保護されたデータを格納します。
- スピン ロック WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 707fc887e3e0a631ffc3cac0777b8cc2e2b20321
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378774"
---
# <a name="providing-storage-for-spin-locks-and-protected-data"></a>スピン ロックおよび保護されたデータ用の記憶域の提供





デバイスのスタートアップの一環として、ドライバーは、スピン ロックで保護されたデータやリソースと、次の場所のいずれかでスピン ロックを対応する常駐のストレージを割り当てる必要があります。

-   デバイス ドライバーを呼び出すことによって設定するオブジェクトのデバイスの拡張機能[ **IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatedevice)

-   呼び出すことによって、ドライバーを設定するコント ローラー オブジェクトのコント ローラー拡張機能[ **IoCreateController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iocreatecontroller)

-   ドライバーを呼び出すことによって取得 nonpaged のシステム領域メモリ[ **exallocatepoolwithtag に**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithtag)

スピン ロックを保持しているときにページング可能なデータにアクセスしようと、そのページが存在しない場合に、致命的なページ フォールトが発生します。 (ページング可能なメモリに格納されたが現在ページ アウト) ため、無効なスピン ロックを参照すると、致命的なページ フォールトまた発生します。

ドライバーでは、各 executive スピン ロックを使用して次のような記憶域を提供する必要があります。

- ドライバーは、明示的に取得しのいずれかを使用して解放するロックをスピンいずれか、 **Ke * Xxx*** ロック ルーチンをスピンします。

- いずれかのいずれかのパラメーターとして使用するロックを回転、 **ExInterlocked * Xxx*** ルーチン。

ドライバーがへの呼び出しを行うときに、 **ExInterlocked * Xxx*** その ISR からルーチンまたは[ *SynchCritSection* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-ksynchronize_routine)ルーチンでは使用できませんのいずれか、 **Ke * Xxx*** ディスパッチより大きい IRQL で取得および解放するルーチンがスピンロック\_レベル。 その結果、呼び出しの間スピン ロックを再利用するドライバー、 **Ke*Xxx*スピンロック**と**ExInterlocked * Xxx*** ルーチンは、IRQL での実行中にすべての呼び出しを行う必要があります&lt;= ディスパッチ\_レベル。

ドライバーに同じスピン ロックを渡すことができます**ExInterlockedInsertHeadList**間は**ExInterlocked * Xxx*** でに 2 つのルーチンは、同じ IRQL でスピン ロックを使用して日常的な。 スピン ロックの使用率がパフォーマンスに与える影響の詳細については、次を参照してください。[スピン ロックを使用します。たとえば](using-spin-locks--an-example.md)します。

Executive スピン ロックをストレージに加え、デバイス ドライバーが multivector ISR または 1 つ以上の ISR. がある場合に、その割り込みオブジェクトに関連するもう 1 つのスピンロックの記憶域を提供する必要があります。

 

 




