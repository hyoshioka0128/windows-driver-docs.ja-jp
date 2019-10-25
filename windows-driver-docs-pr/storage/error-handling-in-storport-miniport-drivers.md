---
title: Storport ミニポート ドライバーでのエラー処理
description: Storport ミニポート ドライバーでのエラー処理
ms.assetid: 23ea8c36-56cf-45ae-a066-765d3a91b542
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4302a93969dffe0f83c66d979aae3d697cc51d99
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844553"
---
# <a name="error-handling-in-storport-miniport-drivers"></a>Storport ミニポート ドライバーでのエラー処理


すべての Storport ミニポートドライバーは、次の種類の SCSI エラーについてシステムポートドライバーに通知する必要があります。 これらのエラーは、ドライバーがエラーの発生時に処理していた SRB を完了する前に、 **Srbstatus**メンバーで設定する必要があります。

-   SRB\_STATUS\_ERROR (HBA が不特定のバスエラーを返した場合)

-   SRB\_の状態\_パリティ\_エラー

-   SRB\_状態\_予期しない\_バス\_無料

-   SRB\_状態\_選択\_タイムアウト

-   SRB\_STATUS\_コマンド\_タイムアウト

-   SRB\_ステータス\_メッセージ\_拒否されました

-   SRB\_状態\_\_デバイスなし

-   SRB\_状態\_\_HBA がありません

-   SRB\_STATUS\_データ\_オーバーラン (アンダーランにも返される)

-   SRB\_ステータス\_フェーズ\_シーケンス\_エラー

-   SRB\_ステータス\_ビジー状態です (TID がビジー状態)

データアンダーランの場合、ミニポートドライバーは、実際に転送されたデータの量を示すために SRB の**Datatransの長さ**を更新する必要があります。

さらに、ミニポートドライバーは、SRB を[**Storportlogerror**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportlogerror)に渡すことによって、上記のエラーのいくつかをログに記録するために、次のガイドラインを使用する必要があります。

Driver writer for SRB\_STATUS\_ERROR の裁量で、エラーをログに記録します。

SRB\_STATUS\_パリティ\_エラーの場合は、常にエラーをログに記録します。

SRB\_状態\_予期しない\_バス\_無料で、常にエラーをログに記録します。

SRB\_STATUS\_SELECTION\_TIMEOUT の場合は、常にエラーを記録します。

SRB\_STATUS\_コマンド\_タイムアウトの場合は、常にエラーをログに記録します。

オーバーランが発生したときではなく、オーバーランが発生したときにデータ\_オーバーランが発生したときに、SRB\_状態\_のエラーをログに記録します。

SRB\_STATUS\_フェーズ\_シーケンス\_エラーが発生した場合は、常にエラーをログに記録します。

ハードウェアエラーが発生した場合は、常に SRB\_STATUS\_BUSY のエラーをログに記録します。

エラーをログに記録するために、ミニポートドライバーは、システム定義の次のいずれかのエラーコードまたは警告コードを使用して[**Storportlogerror**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportlogerror)を呼び出します。

SP\_BUS\_パリティ\_エラーマップを SRB\_ステータス\_パリティ\_エラー

SP\_予期しない\_切断 (ターゲット論理ユニットによる)

SP\_無効\_RESELECTION が SRB\_STATUS\_フェーズ\_SEQUENCE\_FAILURE または SRB\_STATUS\_ERROR にマップされる

SP\_BUS\_TIME\_SRB\_ステータス\_選択\_タイムアウトにマップされる

SP\_REQUEST\_TIMEOUT が SRB\_STATUS\_COMMAND\_TIMEOUT にマップされる

SP\_プロトコル\_エラーが SRB\_状態\_フェーズ\_\_\_\_、SRB\_状態\_予期しない\_バス\_FREE、または SRB 状態データにマップされるオーバーラン条件の\_オーバーラン

SP\_内部\_アダプター\_エラーが SRB\_ステータス\_エラーにマップされる

SP\_IRQ\_\_応答していません (HBA が割り込み要求を生成していないことがミニポートドライバーによって検出されたことを警告します)

SP\_不良\_FW\_FW が*ファームウェア*である)

SP\_不良\_FW\_警告

[**Storportlogerror**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportlogerror)は、エラーログパケットを割り当て、それを設定し、ミニポートドライバーに代わってイベントログに i/o エラーを記録します。 システム管理者またはユーザーは、システムイベントログを調べて、必要に応じて、障害が発生する前に HBA の再構成、修復、または交換を行うことによって、HBA の状態を監視できます。

 

 




