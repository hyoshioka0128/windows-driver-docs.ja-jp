---
title: 転送の非同期処理
description: 転送の非同期処理
ms.assetid: 84b231bd-54ff-4312-8e6c-cfc33e72b8cc
keywords:
- DispatchRead ルーチン
- DispatchWrite ルーチン
- DispatchReadWrite ルーチン
- ディスパッチ ルーチンの WDK カーネル、DispatchReadWrite ルーチン
- ディスパッチ ルーチンの WDK カーネル、DispatchWrite ルーチン
- ディスパッチ ルーチンの WDK カーネル、DispatchRead ルーチン
- 読み取り/書き込みディスパッチ ルーチン WDK カーネル
- IRP_MJ_WRITE I/O 関数のコード
- IRP_MJ_READ I/O 関数のコード
- データ転送の WDK カーネル、読み取り/書き込みディスパッチ ルーチン
- データ転送の WDK カーネル、読み取り/書き込みディスパッチ ルーチン
- 非同期転送 WDK カーネル
- WDK カーネルでは、非同期のデータを転送します。
- WDK カーネルでは、非同期のデータを転送します。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5934d6193d87c05e44fdf7fed8a0609e5961650
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364295"
---
# <a name="handling-transfers-asynchronously"></a>転送の非同期処理





最上位レベルのドライバーを除くすべてのドライバーが処理[ **IRP\_MJ\_読み取り**](https://msdn.microsoft.com/library/windows/hardware/ff550794)と[ **IRP\_MJ\_書き込み** ](https://msdn.microsoft.com/library/windows/hardware/ff550819)非同期的に要求します。 *DispatchRead*と*DispatchWrite*最上位レベルのドライバーもルーチンは、下位レベルのドライバーまたは書き込み要求を非同期の読み取りの処理が完了するを待機できません; などを渡す必要がありますが、下位のドライバーに要求し、状態を返す\_保留します。

同様に、最下位レベルのデバイス ドライバーの*DispatchReadWrite*ルーチンは、転送要求をデバイス I/O 要求を処理し、状態を返す他のドライバー ルーチンを渡す必要があります\_保留します。

高度なドライバー場合があります。 して部分転送 Irp のセットアップが下位のドライバーに渡すこと必要があります。 下位のドライバーによって、部分的な転送の要求が完了したときにのみより高度なドライバーは元読み取り/書き込み IRP を完了できます。

たとえば、SCSI クラス ドライバーの*DispatchReadWrite*ルーチンは部分的な転送要求のセットに基になる HBA の転送機能を超える大きな転送要求を分割するために必要です。 クラス ドライバーは、SCSI ポート/ミニポート ドライバーは、単一の DMA 操作では、各部分転送要求を満たすことができるように、その部分転送の Irp でパラメーターを設定する必要があります。

また、DMA または PIO を使用する他のデバイス ドライバーは自体の大きな転送要求を分割する必要があります。

DMA および PIO の使用に関する詳細については、次を参照してください。[入力/出力手法](i-o-programming-techniques.md)します。

 

 




