---
title: ドライバーのページングの作成
description: ドライバーのページングの作成
ms.assetid: 0b3c1e00-2416-4534-9934-bb05f91c7482
keywords:
- メモリ管理 WDK カーネル、ページング可能ドライバー
- ページング可能ドライバー WDK カーネル
- ページング可能ドライバー WDK カーネル、ページング可能ドライバーの概要
- ページアウトドライバーの WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 13765ab89b7dc329431d73643c271825a781218f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838554"
---
# <a name="making-drivers-pageable"></a>ドライバーのページングの作成





既定では、リンカーは、ドライバーイメージファイルのコードおよびデータセクションに ". text" や ". data" などの名前を割り当てます。 ドライバーが読み込まれると、i/o マネージャーによってこれらのセクションが非ページ化されます。 非ページのセクションは常にメモリに常駐します。

ドライバー開発者は、使用されていないときに Windows がページングファイルにこれらの部分を移動できるように、ドライバーの特定の部分をページング可能にすることができます。 コードまたはデータセクションをページング可能にするために、ドライバー開発者はセクションに "PAGE" で始まる名前を割り当てます。 I/o マネージャーは、ドライバーを読み込むときに、セクションの名前をチェックします。 セクション名が "PAGE" で始まる場合、i/o マネージャーによってセクションがページング可能になります。

IRQL &gt;= ディスパッチ\_レベルで実行されるコードは、メモリ常駐型である必要があります。 つまり、このコードは非ページングセグメント、またはメモリ内でロックされているページング可能なセグメントのいずれかである必要があります。 IRQL &gt;= ディスパッチ\_レベルで実行されているコードでページフォールトが発生すると、バグチェックが行われます。 ドライバーは、ページングされた[ **\_コード**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)マクロを使用して、ページング可能な関数が適切な IRQLs でのみ呼び出されることを確認できます。

コードまたはデータセクションがページング可能な場合、ドライバーは[**MmLockPagableCodeSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmlockpagablecodesection)または[**Mmlockpagabledatasection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmlockpagabledatasection)を呼び出すことによって、メモリ内のセクションをロックできます。 このセクションは、ドライバーが[**MmUnlockPagableImageSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunlockpagableimagesection)ルーチンを呼び出してロックを解除するまで、ロックされたままになります。 ページング可能なセクションはロックされていますが、非ページのセクションと同じように動作します。

コードおよびデータセクションに名前を割り当てる方法については、「 [**MmLockPagableCodeSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmlockpagablecodesection) And [**Mmlockpagabledatasection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmlockpagabledatasection)を参照してください。

ここでは、次のトピックについて説明します。

[コードとデータをページング可能にする必要があるのはどのような場合ですか。](when-should-code-and-data-be-pageable-.md)

[ドライバーコードまたはデータをページング可能にする](making-driver-code-or-data-pageable.md)

 

 




