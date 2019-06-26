---
title: デバイス オブジェクトのフラグの確認
description: デバイス オブジェクトのフラグの確認
ms.assetid: f7bff7b8-bd30-4489-ab3f-ca5ad4d5c1ba
keywords:
- リムーバブル メディアの WDK カーネル、フラグのチェック
- WDK のリムーバブル メディアのフラグ
- デバイス オブジェクトのフラグをチェック
- デバイス オブジェクトのフラグを確認しています
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ea3cea627c87b24ef8c4bffb6d5b24a85deedcc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383365"
---
# <a name="checking-flags-in-the-device-object"></a>デバイス オブジェクトのフラグの確認





各 IRP とリムーバブル メディアからの I/O 操作を要求すると、リムーバブル メディア デバイス ドライバーを決定する必要があるかどうかの操作を行います\_を確認してください\_ボリュームが既に設定されてその**デバイス オブジェクト -&gt;フラグ**します。 この値を設定すると、ドライバーが、次の操作にする必要があります。

-   [ **IRP\_MJ\_読み取り**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)、 [ **IRP\_MJ\_書き込み**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)、および[**IRP\_MJ\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control) 、要求を確認するかどうか SL\_オーバーライド\_を確認してください\_でボリュームが設定されて、**フラグ**のドライバーのメンバー [ **IO\_スタック\_場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)構造体。 場合は、要求された操作を続行します。

    基になるメディアの論理構造に関する情報を返すデバイス制御の要求がある SL\_オーバーライド\_を確認してください\_ボリュームで I/O スタックの場所のセット**フラグ**メンバーと、IFS では、マウントまたはリムーバブル メディア ボリュームを再マウントします。

-   対応するドライブ、デバイス、または操作を実行中にパーティションの I/O 要求を実行するために、ドライバーを拒否する必要がありますそれ以外の場合、\_を確認してください\_でボリュームが設定されてその**デバイス オブジェクト -&gt;フラグ**します。 リムーバブル メディアのドライバーが繰り返す手順 3 と 4 に、FSD が解除されるまで各 IRP の両方を行う前のサブセクションで説明されていると、対応するデバイスに送信 Irp に失敗する必要があります\_確認\_リムーバブル メディア ドライバーのボリューム**デバイス オブジェクト -&gt;フラグ**します。

リムーバブル メディア デバイス ドライバーが Irp が失敗しない場合と\_を確認してください\_ボリュームが設定され SL\_オーバーライド\_を確認してください\_前の転送要求のボリュームが設定されていない、ファイル システムのことができますキャッシュされたファイル データの整合性を維持でも原因ユーザーに、開いているファイルを保持するメディアを再マウントするように求められます。

 

 




