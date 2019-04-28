---
title: SCSI ミニポート ドライバーでのエラー処理
description: SCSI ミニポート ドライバーでのエラー処理
ms.assetid: 0d9a2d60-c8e5-48f6-9c1f-d593e59095c8
keywords:
- SCSI ミニポート ドライバー WDK ストレージのエラー
- エラー WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6aa30e3280f1d33d6f9ad939e20172118b125901
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380507"
---
# <a name="error-handling-in-scsi-miniport-drivers"></a>SCSI ミニポート ドライバーでのエラー処理


## <span id="ddk_error_handling_in_scsi_miniport_drivers_kg"></span><span id="DDK_ERROR_HANDLING_IN_SCSI_MINIPORT_DRIVERS_KG"></span>


すべての SCSI ミニポート ドライバーには、SCSI エラーの次の種類について、システム ポートのドライバーを通知する必要があります。 これらのエラーを設定する必要があります、 **SrbStatus**メンバー、ドライバーはエラーが発生したときに処理されて SRB を完了する前に。

-   SRB\_状態\_(、HBA は、不特定のバス エラーを返す) 場合のエラー

-   SRB\_状態\_パリティ\_エラー

-   SRB\_状態\_予期しない\_BUS\_FREE

-   SRB\_状態\_選択\_タイムアウト

-   SRB\_状態\_コマンド\_タイムアウト

-   SRB\_状態\_メッセージ\_拒否済み

-   SRB\_状態\_いいえ\_デバイス

-   SRB\_状態\_いいえ\_HBA

-   SRB\_状態\_データ\_オーバーラン (アンダーランに対しても返されます)

-   SRB\_状態\_フェーズ\_シーケンス\_エラー

-   SRB\_状態\_BUSY (ビジー TID)

データの不足、ミニポート ドライバーを SRB の更新する必要があります**DataTransferLength**を実際にどのくらいのデータは転送されたかを示します。

さらに、ミニポート ドライバーに SRB を渡すことによって、上記のエラーの一部を記録する、次のガイドラインを使用する必要があります[ **ScsiPortLogError**](https://msdn.microsoft.com/library/windows/hardware/ff564652):

SRB のドライバーの作成者の判断でエラー ログに記録\_状態\_エラー。

SRB のエラー ログを常に\_状態\_パリティ\_エラー。

SRB のエラー ログを常に\_状態\_予期しない\_BUS\_無料。

SRB のエラー ログを常に\_状態\_選択\_タイムアウトします。

SRB のエラー ログを常に\_状態\_コマンド\_タイムアウトします。

SRB のエラー ログに記録\_状態\_データ\_オーバーランしないときはアンダーランがオーバーランが発生するたびに発生します。

SRB のエラー ログを常に\_状態\_フェーズ\_シーケンス\_失敗します。

SRB のエラー ログを常に\_状態\_でハードウェア エラー ビジーです。

ミニポート ドライバーの呼び出しエラーをログに記録する[ **ScsiPortLogError** ](https://msdn.microsoft.com/library/windows/hardware/ff564652)次のシステム定義のエラーまたは警告コードのいずれかを使用します。

SP\_BUS\_パリティ\_エラーにマップ SRB\_状態\_パリティ\_エラー

SP\_予期しない\_(ターゲット論理ユニット) での切断

SP\_無効な\_済マップ SRB\_状態\_フェーズ\_シーケンス\_障害または SRB\_状態\_エラー

SP\_BUS\_時間\_アウト マップ SRB\_状態\_選択\_タイムアウト

SP\_要求\_SRB にタイムアウトがマップ\_状態\_コマンド\_タイムアウト

SP\_プロトコル\_SRB にエラーがマップ\_状態\_フェーズ\_選択\_エラー、SRB\_状態\_予期しない\_BUS\_FREE、または SRB\_状態\_データ\_オーバーランの状態のオーバーラン

SP\_内部\_アダプター\_エラーにマップ SRB\_状態\_エラー

SP\_IRQ\_いない\_応答 (警告、ミニポート ドライバーが検出された HBA が不要になったの割り込み要求を生成していること)

SP\_不良\_FW\_エラー (FW が*ファームウェア*)

SP\_不良\_FW\_警告

[**ScsiPortLogError** ](https://msdn.microsoft.com/library/windows/hardware/ff564652)エラー ログのパケットを割り当てます、設定、およびミニポート ドライバーに代わってイベント ログに I/O エラーを記録します。 システム管理者またはユーザーの場合は、システム イベント ログを確認し、必要に応じて、再構成、修復、または失敗する前に、HBA を交換して HBA の状態を監視できます。

 

 




