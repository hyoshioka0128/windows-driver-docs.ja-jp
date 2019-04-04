---
title: Storport ミニポート ドライバー、Storport のインターフェイス
description: Storport ミニポート ドライバー、Storport のインターフェイス
ms.assetid: 8e09d6a6-7e4f-44fc-a2b0-5f21b4ac0593
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90c43df04cdedd9d8f93d53aad2969b94abe8607
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559381"
---
# <a name="storports-interface-with-storport-miniport-drivers"></a>Storport ミニポート ドライバー、Storport のインターフェイス


Storport ドライバー、Storport ミニポート ドライバーの間の通信が行わによって SCSI 要求のブロック (される Srb) およびミニポート ドライバー コールバック ルーチン。 Storport ミニポート ドライバー コールバック ルーチンの詳細については、[Storport ドライバー ミニポート ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff567543)を参照してください。

概要と SRB の個々 の関数、SRB フラグ、および SRB 状態の値の定義については、[ **SCSI\_要求\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff565393)を参照してください。

ミニポート ドライバーが SRB 関数に対応する方法に関する話題は、[ **HwStorStartIo**](https://msdn.microsoft.com/library/windows/hardware/ff557423)を参照してください。

Storport は、される Srb を Storport ミニポート ドライバーで非同期処理のために転送します。 通常、ミニポート ドライバーには、実際には、要求を完了するまでに時間がかかります。 タグが付けられたキューをサポートするホスト バス アダプターでは、内部要求キューに配置でき、Storport を各要求に割り当てることのタグで示される順序で処理することができます。 [ **SCSI\_要求\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff565393) (SRB) 構造体には、Storport ドライバーを使用して、ホスト アダプターの内部キューでされる Srb を順序付けする方法を指定する 2 つのメンバーが含まれています。:**QueuedTag**と**QueueAction**します。 Storport 割り当てます、カウントまたは *「タグ」* 値に、 **QueuedTag**アダプターが、パケットを処理する順序を示す各 SRB のメンバー。 タグの値では、Storport される Srb が正常に完了してされる Srb がタイムアウトしたかを追跡することもできます。

**QueueAction**値は次のいずれかのメンバーが割り当てられます。

SRB\_単純\_タグ\_要求

SRB\_ヘッド\_の\_キュー\_タグ\_要求

SRB\_ORDERED\_キュー\_タグ\_要求

これらの値の詳細については、scsi-3 仕様を参照してください。

 

 




