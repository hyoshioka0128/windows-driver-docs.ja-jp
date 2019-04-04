---
title: 記憶域周辺機器への要求の処理
description: 記憶域周辺機器への要求の処理
ms.assetid: 3859588e-fc39-4323-a901-8771874e64d2
keywords:
- 記憶域クラス ドライバー WDK、周辺機器
- クラスのドライバー WDK の記憶域、周辺機器
- 周辺機器の WDK ストレージ
- 記憶域周辺機器 WDK
- 記憶域周辺機器について、周辺機器の WDK ストレージ
- 記憶域周辺機器 WDK、記憶域周辺機器について
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b52d7c5a34f4d9d02434ed301d83a436896111df
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579801"
---
# <a name="handling-requests-to-storage-peripherals"></a>記憶域周辺機器への要求の処理


## <span id="ddk_handling_requests_to_storage_peripherals_kg"></span><span id="DDK_HANDLING_REQUESTS_TO_STORAGE_PERIPHERALS_KG"></span>


基になるバス経由で要求を実行する記憶域ポート ドライバーを必要とするすべての要求、クラス ドライバーは IRP を SCSI 要求 SCSI コマンド記述子ブロック (CDB) を格納しているブロック (SRB) でする必要があります設定します。 その結果、ほとんどのストレージ クラス ドライバーがある 1 つまたは複数の内部*BuildRequest*される Srb を構築するためのルーチンです。 このようなルーチンの詳細については、[記憶域クラス ドライバー BuildRequest ルーチン](storage-class-driver-s-buildrequest-routine.md)を参照してください。

記憶域クラス ドライバーは IRP でも渡す\_MJ\_基になるストレージ ポート ドライバーに SCSI 要求。 このような要求から発生すること、[ストレージ フィルター ドライバー](storage-filter-drivers.md)。

[ **IOCTL\_SCSI\_渡す\_を通じて**](https://msdn.microsoft.com/library/windows/hardware/ff560519)で説明されている要求[SCSI パススルー要求の処理](handling-scsi-pass-through-requests.md)、クラスドライバーは、設定、 **MinorFunction**コード IRP を\_MJ\_デバイス\_IRPを渡す前にIRPのポートドライバーのI/Oスタックの場所でコントロール\_MJ\_デバイス\_コントロール要求を使用してドライバーをポート[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)します。

すべての記憶域クラス ドライバーは、転送要求を分割することを担当 (IRP\_MJ\_読み取りや IRP\_MJ\_書き込み) を基になる HBA の機能を超えます。 その結果、ほとんどのクラス ドライバーを呼び出すことも内部*SplitTransferRequest*ルーチンを記載[記憶域クラス ドライバー SplitTransferRequest ルーチン](storage-class-driver-s-splittransferrequest-routine.md)、または同じ機能を実装用のディスパッチ ルーチンは、読み取りおよび書き込み要求。

記憶域周辺機器への要求の処理についての詳細については、次のトピックを参照してください。

[SCSI パススルーの要求の処理](handling-scsi-pass-through-requests.md)

[記憶域周辺機器に PnP 要求の処理](handling-pnp-requests-to-storage-peripherals.md)

[記憶域周辺機器に電力要求を処理](handling-power-requests-to-storage-peripherals.md)

[ストレージ要求のキュー](queuing-storage-requests.md)

 

 




