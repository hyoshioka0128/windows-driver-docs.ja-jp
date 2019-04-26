---
title: 停止したドライバーとタイムアウトの分析
description: 停止したドライバーとタイムアウトの分析
ms.assetid: c305acba-48b9-4597-925a-8b1ded4f0048
keywords:
- SCSI ミニポート デバッグ、ハング、タイムアウト
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 191bda869710e14d445e68722da54c06c9d08290
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355410"
---
# <a name="analyzing-stalled-drivers-and-time-outs"></a>停止したドライバーとタイムアウトの分析


SCSI ミニポート ドライバーをデバッグするときにハングするには 3 つの最も一般的な原因し、タイムアウトは。

-   SCSI ミニポート DPC が実行されていません

-   次の要求に要求が失敗した SCSI ミニポート

-   SCSI ミニポートによって、要求が終了しない、通常を待機しているためマップ登録されます。

SCSI ミニポート DPC が実行されていないことが疑われる場合は、使用[ **! pcr** ](-pcr.md)現在のプロセッサの DPC キューを表示します。 SCSI ポート DPC ルーチンが DPC キューにある場合は、このルーチンがこれまでと呼ばれるかどうかを判断するには、このルーチンで、ブレークポイントを設定します。 それ以外の場合、使用[ **! scsikd.scsiext** ](-scsikd-scsiext.md)各デバイスにします。 次のサンプル出力を検討してください、 **! scsikd.scsiext**拡張機能。

```dbgcmd
0: kd> !scsikd.scsiext 86353040 
Common Extension:
   < ..omitted.. >
Logical Unit Extension:
  Address (3, 0, 1, 0) Claimed  Enumerated Visible
  LuFlags (0x00000000):
  Retry 0x00          Key 0x008889ff
  Lock 0x00000000  Pause 0x00000000   CurrentLock: 0x00000000
  HwLuExt 0x862e6f00  Adapter 0x8633db28  Timeout 0x0000000a
  NextLun 0x00000000  ReadyLun 0x00000000
  Pending 0x00000000  Busy 0x00000000     Untagged 0x00000000
 
  . . .  
 
Request list @0x86353200:
      Tick count is 2526
      SrbData 8615d700  Srb 8611f4fc  Irp 8611f2b8   Key 60197  <1s
      SrbData 85e72868  Srb 86100c3c Irp 861009f8   Key e29dc7  <1s 
```

タイムアウトのスロットは、-1 とタグなしのスロットが 0 以外の場合、またはタイムアウト スロットが 0 以外と表示要求がある、ミニポートが失敗した場合、次の要求を要求します。

または場合再試行スロットとビジー状態のスロットは、0 以外の場合は、要求が完了しません SCSI ミニポートによってマップ レジスタを待機しているため。 同様に、タグ付けされていないと保留中のスロットは、0 以外の場合は、マップのレジスタを SCSI ミニポートを待機して可能性があります。 どちらの場合は、SCSI 要求のブロック (SRB) のアドレスは、ビジー状態のスロット内のアドレスとが完了しなかった要求のアドレスです。 SRB の詳細については、使用、 [ **! minipkd.srb** ](-minipkd-srb.md)このアドレスを入力として使用して拡張機能。

[ **! Devobj** ](-devobj.md)拡張機能は、SCSI ミニポートでマップを登録するを待機しているかどうかを決定します。 入力として、要求を発行しているデバイスのデバイス オブジェクトのアドレスを使用して、 **! devobj**します。 現在の IRQ が 0 以外の場合は、マップのレジスタの SCSI ミニポートが待機している可能性が高いです。

 

 





