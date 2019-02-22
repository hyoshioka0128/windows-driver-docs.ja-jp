---
title: ドライバーのページングを行う
description: ドライバーのページングを行う
ms.assetid: 0b3c1e00-2416-4534-9934-bb05f91c7482
keywords:
- メモリ管理の WDK カーネル、ページング可能なドライバー
- ページング可能なドライバー WDK カーネル
- ページング可能なドライバー WDK カーネルでは、ページング可能なドライバーについて
- ページ アウト ドライバー WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7723e1cbf3e98586836b0b74d90f88952aa84abf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556521"
---
# <a name="making-drivers-pageable"></a>ドライバーのページングを行う





既定では、リンカーは、ドライバーのイメージ ファイルのコードとデータのセクションに".text"と".data"などの名前を割り当てます。 ドライバーが読み込まれるときに I/O マネージャーにより、これらのセクションでは非ページ。 非ページ セクションは、メモリ常駐型では常にします。

ドライバーの開発者には、Windows は、使用されていないときに、ページング ファイルへのこれらのパーツを移動できるように、ドライバーの指定されたパーツをページングするオプションがあります。 コードまたはデータ セクションにページングするに、ドライバー開発者がセクションに「ページ」で始まる名前を割り当てます。 ドライバーの読み込み時に、I/O マネージャーは、セクションの名前を確認します。 セクション名は、「ページ」で始まっている場合、I/O マネージャーによるセクション ページング可能です。

IRQL で実行されるコード&gt;= ディスパッチ\_レベルはメモリ常駐型である必要があります。 つまり、このコードには、非ページング セグメント、またはメモリにロックされているページング可能なセグメントがあります。 場合 IRQL で実行されているコード&gt;= ディスパッチ\_レベルでは、ページ フォールト、バグ チェックが行われます。 ドライバーを使用できる、 [**ページ\_コード**](https://msdn.microsoft.com/library/windows/hardware/ff558773)マクロをページング可能な関数が適切な Irql でのみ呼び出されることを確認します。

コードまたはデータ セクションがページング可能な場合は、ドライバーが呼び出すことによってメモリ内のセクションをロックできます、 [ **MmLockPagableCodeSection** ](https://msdn.microsoft.com/library/windows/hardware/ff554601)または[ **MmLockPagableDataSection**](https://msdn.microsoft.com/library/windows/hardware/ff554607)ルーチン。 セクションがロックされたままドライバー呼び出されるまで、 [ **MmUnlockPagableImageSection** ](https://msdn.microsoft.com/library/windows/hardware/ff556377)ロックを解除するルーチン。 ページング可能なセクションがロックされている間は、非ページ セクションと同じ動作します。

コードとデータ セクションに名前を割り当てる方法については、次を参照してください[ **MmLockPagableCodeSection** ](https://msdn.microsoft.com/library/windows/hardware/ff554601)と[ **MmLockPagableDataSection** 。](https://msdn.microsoft.com/library/windows/hardware/ff554607).

ここでは、次のトピックについて説明します。

[ときにコードとデータべきページング可能でしょうか。](when-should-code-and-data-be-pageable-.md)

[ドライバー コードまたはデータをページング可能にします。](making-driver-code-or-data-pageable.md)

 

 




