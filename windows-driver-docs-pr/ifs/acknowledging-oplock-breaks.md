---
title: Oplock の破損の確認
description: Oplock の破損の確認
ms.assetid: ea5bcd1e-d22c-4f80-89e4-1a61e43959dd
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2aa2a988f24e33c145ad24d075f71f334751c7f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323228"
---
# <a name="acknowledging-oplock-breaks"></a>Oplock の破損の確認


## <span id="oplock_break_conditions"></span><span id="OPLOCK_BREAK_CONDITIONS"></span>


Oplock の所有者を返すことができる受信確認のさまざまな種類があります。 ような[要求を許可](granting-oplocks.md)、ファイル システムの制御コードとしてこれらの受信確認が送信されます (つまり、 [FSCTL](https://go.microsoft.com/fwlink/p/?linkid=124238)秒)。 それらは以下のとおりです。

-   FSCTL\_OPLOCK\_中断\_ACKNOWLEDGE
    -   この FSCTL では、oplock の所有者には、ストリームの同期が完了したこと、およびレベル (レベル 2 または None) の分割、oplock を承諾することを示します。
-   FSCTL\_OPLOCK\_中断\_ACK\_いいえ\_2
    -   この FSCTL は、oplock の所有者がストリームの同期は完了しましたが、レベル 2 oplock はしないことを示します。 代わりに、oplock を None に壊れたにする (つまり、oplock が完全に解除される)。
-   FSCTL\_OPBATCH\_ACK\_閉じる\_PENDING
    -   Oplock の所有者がストリームの同期が完了し、oplock を完全に放棄はレベル 1 の oplock のこの FSCTL を示します (レベル 2 oplock 可能性がないこの受信確認)。

    <!-- -->

    -   バッチまたはフィルターの oplock の場合は、この FSCTL oplock の所有者が、oplock が付与されたストリームのハンドルを終了しようとしたことを示します。 Oplock の受信確認を待機しています。 ブロックされている操作は、oplock の所有者のハンドルが閉じられるまでの待機に進みます。
-   FSCTL\_要求\_OPLOCK
    -   要求を指定することによって\_OPLOCK\_入力\_フラグ\_で ACK、**フラグ**メンバー要求の\_OPLOCK\_入力\_バッファーとして渡された構造体、 *lpInBuffer*パラメーターの[DeviceIoControl](https://go.microsoft.com/fwlink/p/?linkid=124239)、この FSCTL は Windows 7 の各 oplock の区切りを確認するために使用します。 受信確認は必要な場合にのみ要求\_OPLOCK\_出力\_フラグ\_ACK\_必須フラグが設定されて、**フラグ**要求のメンバー\_OPLOCK\_出力\_として渡されたバッファーの構造、 *lpOutBuffer*パラメーターの[DeviceIoControl](https://go.microsoft.com/fwlink/p/?linkid=124239)します。 同様の方法で[ **FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)と[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)をカーネル モードから Windows 7 の各 oplock のことを確認するために使用できます。 詳細については、次を参照してください。 [ **FSCTL\_要求\_OPLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff545530)します。

A 関連 FSCTL コードは FSCTL\_OPLOCK\_中断\_に通知します。 このコードは、呼び出し元が指定のストリームに oplock が完了したときに通知するときに使用されます。 この呼び出しはブロック可能性があります。 ときに FSCTL\_OPLOCK\_中断\_通知呼び出しのステータスを返します\_成功した場合、このことを示します、次のいずれか。

-   Oplock が与えられていません。

-   Oplock されなかった進行中の呼び出し時にします。

-   進行中であった任意 oplock が完了しました。

受信確認の送信には、エラーと受信確認の状態と FSCTL IRP が失敗受信確認が必要ない場合は\_無効な\_OPLOCK\_プロトコル。

Oplock が要求されるファイルのハンドルを閉じると、中断が暗黙的に確認されます。 共有違反の oplock の場合、oplock の所有者は、oplock が承認されると、ファイルのハンドルを閉じるし、ファイルの他のユーザーの共有違反を防ぐため。

 

 




