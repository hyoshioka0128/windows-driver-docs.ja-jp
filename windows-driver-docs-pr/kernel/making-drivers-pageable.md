---
title: ドライバーをページング可能にする
description: ドライバーをページング可能にする
ms.assetid: 0b3c1e00-2416-4534-9934-bb05f91c7482
keywords:
- メモリ管理の WDK カーネル、ページング可能なドライバー
- ページング可能なドライバー WDK カーネル
- ページング可能なドライバー WDK カーネルでは、ページング可能なドライバーについて
- ページ アウト ドライバー WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 68f09c46356267826a27971a1912ec48697110ba
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365806"
---
# <a name="making-drivers-pageable"></a>ドライバーをページング可能にする





既定では、リンカーは、ドライバーのイメージ ファイルのコードとデータのセクションに".text"と".data"などの名前を割り当てます。 ドライバーが読み込まれるときに I/O マネージャーにより、これらのセクションでは非ページ。 非ページ セクションは、メモリ常駐型では常にします。

ドライバーの開発者には、Windows は、使用されていないときに、ページング ファイルへのこれらのパーツを移動できるように、ドライバーの指定されたパーツをページングするオプションがあります。 コードまたはデータ セクションにページングするに、ドライバー開発者がセクションに「ページ」で始まる名前を割り当てます。 ドライバーの読み込み時に、I/O マネージャーは、セクションの名前を確認します。 セクション名は、「ページ」で始まっている場合、I/O マネージャーによるセクション ページング可能です。

IRQL で実行されるコード&gt;= ディスパッチ\_レベルはメモリ常駐型である必要があります。 つまり、このコードには、非ページング セグメント、またはメモリにロックされているページング可能なセグメントがあります。 場合 IRQL で実行されているコード&gt;= ディスパッチ\_レベルでは、ページ フォールト、バグ チェックが行われます。 ドライバーを使用できる、 [**ページ\_コード**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)マクロをページング可能な関数が適切な Irql でのみ呼び出されることを確認します。

コードまたはデータ セクションがページング可能な場合は、ドライバーが呼び出すことによってメモリ内のセクションをロックできます、 [ **MmLockPagableCodeSection** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmlockpagablecodesection)または[ **MmLockPagableDataSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmlockpagabledatasection)ルーチン。 セクションがロックされたままドライバー呼び出されるまで、 [ **MmUnlockPagableImageSection** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmunlockpagableimagesection)ロックを解除するルーチン。 ページング可能なセクションがロックされている間は、非ページ セクションと同じ動作します。

コードとデータ セクションに名前を割り当てる方法については、次を参照してください[ **MmLockPagableCodeSection** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmlockpagablecodesection)と[ **MmLockPagableDataSection** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmlockpagabledatasection)。

ここでは、次のトピックについて説明します。

[ときにコードとデータべきページング可能でしょうか。](when-should-code-and-data-be-pageable-.md)

[ドライバー コードまたはデータをページング可能にします。](making-driver-code-or-data-pageable.md)

 

 




