---
title: SCSI ミニポート デバッグするためのバグ チェック
description: SCSI ミニポート デバッグするためのバグ チェック
ms.assetid: 9a517096-f708-452b-83f6-e7d4f0d41ac3
keywords:
- デバッグ SCSI ミニポート、バグを確認します
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23de7d56bfd920a681e740b3808325461ed05e1c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538772"
---
# <a name="bug-checks-for-scsi-miniport-debugging"></a>SCSI ミニポート デバッグするためのバグ チェック


SCSI ミニポート ドライバーをデバッグ中に生じる主に 2 つのバグ チェックが: バグ チェック 0x77 (カーネル\_スタック\_インページ\_エラー) とバグ チェック 0x7A (カーネル\_データ\_インページ\_エラー)。 そのパラメーターの詳細については、次を参照してください。 [**バグ チェック 0x77** ](bug-check-0x77--kernel-stack-inpage-error.md)と[**バグ チェック 0x7A**](bug-check-0x7a--kernel-data-inpage-error.md)します。

これらのバグ チェックのそれぞれは、ページングのエラーが発生したことを示します。 これらのバグ チェックの 3 つの主な原因があります。

-   完全なバスのリセットにより、特定のデバイス上のタイムアウトまたはアダプターのアクティビティがありません。

-   選択範囲のタイムアウト

-   コント ローラーのエラー

失敗の正確な原因を確認するのを使用して開始、 [ **! scsikd.classext** ](-scsikd-classext.md) SRB 状態、SCSI の状態など、最近失敗した要求に関する情報を表示する拡張機能と要求のデータを意味します。

```dbgcmd
kd> !scsikd.classext 816e96b0
Storage class device 816e96b0 with extension at 816e9768

Classpnp Internal Information at 817b4008

    Failed requests:

           Srb    Scsi
    Opcode Status Status Sense Code  Sector   Time  Stamp
    ------ ------ ------ ---------- -------- ------------
      2a     0a     02    03 0c 00  0000abcd 23:01:07.453  Retried
      28     0a     02    03 04 00  0000abcd 23:01:07.984  Retried

dt classpnp!_CLASS_PRIVATE_FDO_DATA 817b4008 -

...
```

前の例では、オペコード 0x2A が、書き込み操作に示し、0x28 が読み取り操作を示します。 この例の SCSI 状態は、条件の確認を示すを 02 にです。 センス コードでは、詳細なエラー情報を提供します。

いつものようにミニポート ドライバー開発者は、SRB のステータス コードをハードウェアのエラー コードを関連付けることを担当します。 通常、タイムアウトは SRB 0x0A、選択範囲のタイムアウトのコードに関連付けられます。 SRB 0x0e がフルのバスのリセットに通常関連付けには、コント ローラーのエラーに関連付けられていることもできます。

 

 





