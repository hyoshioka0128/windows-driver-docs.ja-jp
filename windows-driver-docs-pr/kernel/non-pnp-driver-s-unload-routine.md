---
title: PnP 以外のドライバーのアンロードルーチン
description: PnP 以外のドライバーのアンロードルーチン
ms.assetid: 5917648f-1e7e-4b39-9aa6-d6cdaac7a2cd
keywords:
- アンロードルーチン WDK カーネル、非 PnP ドライバー
- PnP 以外のアンロードルーチン WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55571112e6ad636197fa93443c16064be2d6763d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838537"
---
# <a name="non-pnp-drivers-unload-routine"></a>PnP 以外のドライバーのアンロードルーチン





PnP デバイスの削除要求を処理しない、以前のドライバーと高レベルのファイルシステムドライバーでは、リソースを解放し、デバイスオブジェクトを削除して、[*アンロード*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)ルーチンでデバイススタックからデタッチする必要があります。

まだ実行していない場合は、デバイスからの割り込みを無効にすることによって、従来のデバイスドライバーが*アンロード*ルーチンで最初に実行する必要があります。 それ以外の場合、その ISR はデバイスの割り込みを処理するために呼び出されますが、*アンロード*ルーチンは、その割り込みを処理する必要があるデバイス拡張機能のリソースを解放します。 このような状況で ISR が正常に実行されている場合でも、 [*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)または[*CUSTOMDPC*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine)ルーチン (isr がキューに登録している場合) や、IRQL &gt;= ディスパッチ\_レベルで実行される可能性のある他のドライバールーチンは、*アンロード*の前に実行されます。ルーチンが再び制御を取り戻すと、別のドライバールーチンが参照するリソースを*アンロード*ルーチンが削除した可能性が高まります。 詳細については、「[ハードウェアの優先順位の管理](managing-hardware-priorities.md)」を参照してください。

割り込みを無効にした後、ファイルシステムとレガシドライバーはリソースとオブジェクトを解放する必要があります。 詳細については、次の2つのセクションを参照してください。

[ドライバーで割り当てられたリソースの解放](releasing-driver-allocated-resources.md)

[デバイスとコントローラーオブジェクトの解放](releasing-device-and-controller-objects.md)

 

 




