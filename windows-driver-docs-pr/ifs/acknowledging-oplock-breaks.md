---
title: Oplock の破損の確認
description: Oplock の破損の確認
ms.assetid: ea5bcd1e-d22c-4f80-89e4-1a61e43959dd
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 990be83f5b82e089aabc7304df4ff82cacee51d0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841496"
---
# <a name="acknowledging-oplock-breaks"></a>Oplock の破損の確認


## <span id="oplock_break_conditions"></span><span id="OPLOCK_BREAK_CONDITIONS"></span>


Oplock の所有者は、さまざまな種類の受信確認を返すことができます。 [Grant 要求](granting-oplocks.md)と同様に、これらの受信確認はファイルシステム制御コード (つまり[FSCTL](https://go.microsoft.com/fwlink/p/?linkid=124238)s) として送信されます。 それらは以下のとおりです。

-   FSCTL\_OPLOCK\_中断\_確認
    -   この FSCTL は、oplock 所有者がストリーム同期を完了し、oplock が解除されたレベル (レベル2または None のいずれか) を受け入れることを示します。
-   FSCTL\_OPLOCK\_中断\_ACK\_NO\_2
    -   この FSCTL は、oplock 所有者がストリーム同期を完了したが、レベル2の oplock を必要としないことを示します。 代わりに、oplock は None に分割する必要があります (つまり、oplock は完全に放棄)。
-   FSCTL\_OPBATCH\_ACK\_終了\_保留中
    -   レベル1の oplock の場合、この FSCTL は oplock の所有者がストリームの同期を完了し、oplock が完全に保っままされていることを示します (この確認によってレベル2の oplock が生成されることはありません)。

    <!-- -->

    -   バッチまたはフィルターの oplock の場合、この FSCTL は oplock 所有者が oplock が付与されたストリームハンドルを閉じることを示します。 Oplock 解除の確認を待機している操作がブロックされた場合は、oplock 所有者のハンドルが閉じられるまで待機し続けます。
-   FSCTL\_要求\_OPLOCK
    -   要求\_OPLOCK を指定することによって、要求の**Flags**メンバーで\_入力\_フラグ\_ACK を指定することにより、 [DeviceIoControl](https://go.microsoft.com/fwlink/p/?linkid=124239)の*lpinbuffer*パラメーターとして渡される入力\_バッファー構造体\_この FSCTL を使用して、Windows 7 の oplock が解除されたことを確認します。\_ 受信確認が必要なのは、要求の Flags メンバーで\_出力\_フラグ\_ACK\_必要フラグが設定されている場合にのみ、要求の**フラグ**メンバー\_OPLOCK\_出力\_バッファー構造として渡される\_[DeviceIoControl](https://go.microsoft.com/fwlink/p/?linkid=124239)の*lpoutbuffer*パラメーター。 同様の方法で、 [**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)と[**zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)を使用して、カーネルモードからの Windows 7 の oplock を確認することができます。 詳細については、「 [**FSCTL\_REQUEST\_OPLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsctl-request-oplock)」を参照してください。

関連する FSCTL コードは FSCTL\_OPLOCK\_中断\_通知します。 このコードは、指定されたストリームで oplock の解除が完了したときに呼び出し元が通知を受け取る場合に使用されます。 この呼び出しはブロックされる可能性があります。 FSCTL\_OPLOCK\_中断\_通知呼び出しが成功\_ステータスを返した場合は、次のいずれかが返されます。

-   Oplock は付与されません。

-   呼び出し時に oplock 解除が実行されていませんでした。

-   進行中の oplock の中断がすべて完了しました。

受信確認が想定されていないときに受信確認を送信すると、エラーが発生し、受信確認 FSCTL IRP が失敗し、状態\_無効\_OPLOCK\_プロトコルになります。

Oplock 解除が要求されたファイルのハンドルを閉じると、暗黙的に中断が認識されます。 Oplock が共有違反に対して中断された場合、oplock 所有者は oplock 解除を確認し、ファイルの他のユーザーの共有違反を防ぐファイルハンドルを閉じることができます。

 

 




