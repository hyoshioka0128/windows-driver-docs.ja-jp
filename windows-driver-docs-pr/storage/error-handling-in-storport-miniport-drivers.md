---
title: Storport ミニポート ドライバーでのエラー処理
description: Storport ミニポート ドライバーでのエラー処理
ms.assetid: 23ea8c36-56cf-45ae-a066-765d3a91b542
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66c33442cf327b37573a94c10198fcf60bc96bb7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369576"
---
# <a name="error-handling-in-storport-miniport-drivers"></a>Storport ミニポート ドライバーでのエラー処理


すべて Storport ミニポート ドライバーでは、SCSI エラーの次の種類について、システム ポートのドライバーを通知する必要があります。 これらのエラーを設定する必要があります、 **SrbStatus**メンバー、ドライバーはエラーが発生したときに処理されて SRB を完了する前に。

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

さらに、ミニポート ドライバーに SRB を渡すことによって、上記のエラーの一部を記録する、次のガイドラインを使用する必要があります[ **StorPortLogError**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportlogerror):

SRB のドライバーの作成者の判断でエラー ログに記録\_状態\_エラー。

SRB のエラー ログを常に\_状態\_パリティ\_エラー。

SRB のエラー ログを常に\_状態\_予期しない\_BUS\_無料。

SRB のエラー ログを常に\_状態\_選択\_タイムアウトします。

SRB のエラー ログを常に\_状態\_コマンド\_タイムアウトします。

SRB のエラー ログに記録\_状態\_データ\_オーバーランしないときはアンダーランがオーバーランが発生するたびに発生します。

SRB のエラー ログを常に\_状態\_フェーズ\_シーケンス\_失敗します。

SRB のエラー ログを常に\_状態\_でハードウェア エラー ビジーです。

ミニポート ドライバーの呼び出しエラーをログに記録する[ **StorPortLogError** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportlogerror)次のシステム定義のエラーまたは警告コードのいずれかを使用します。

SP\_BUS\_パリティ\_エラーにマップ SRB\_状態\_パリティ\_エラー

SP\_予期しない\_(ターゲット論理ユニット) での切断

SP\_無効な\_済マップ SRB\_状態\_フェーズ\_シーケンス\_障害または SRB\_状態\_エラー

SP\_BUS\_時間\_アウト マップ SRB\_状態\_選択\_タイムアウト

SP\_要求\_SRB にタイムアウトがマップ\_状態\_コマンド\_タイムアウト

SP\_プロトコル\_SRB にエラーがマップ\_状態\_フェーズ\_選択\_エラー、SRB\_状態\_予期しない\_BUS\_FREE、または SRB\_状態\_データ\_オーバーランの状態のオーバーラン

SP\_内部\_アダプター\_エラーにマップ SRB\_状態\_エラー

SP\_IRQ\_いない\_応答 (警告、ミニポート ドライバーが検出された HBA が不要になったの割り込み要求を生成していること)

SP\_不良\_FW\_FW があるエラー*ファームウェア*)

SP\_不良\_FW\_警告

[**StorPortLogError** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportlogerror)エラー ログのパケットを割り当てます、設定、およびミニポート ドライバーに代わってイベント ログに I/O エラーを記録します。 システム管理者またはユーザーの場合は、システム イベント ログを確認し、必要に応じて、再構成、修復、または失敗する前に、HBA を交換して HBA の状態を監視できます。

 

 




