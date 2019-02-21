---
title: もう一度設定と HwScsiFindAdapter から取得
description: もう一度設定と HwScsiFindAdapter から取得
ms.assetid: 8a9cde40-06fa-4b56-818d-63a9c71da208
keywords:
- HwScsiFindAdapter
- SCSI ミニポート ドライバー WDK ストレージ、HwScsiFindAdapter
- もう一度 WDK SCSI
- WDK SCSI の値を返す
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab5e5294d49243fe708b76837135ac9f5b647133
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558448"
---
# <a name="setting-again-and-returning-from-hwscsifindadapter"></a>もう一度設定と HwScsiFindAdapter から取得


## <span id="ddk_setting_again_and_returning_from_hwscsifindadapter_kg"></span><span id="DDK_SETTING_AGAIN_AND_RETURNING_FROM_HWSCSIFINDADAPTER_KG"></span>


サポートされており、正常に構成された HBA の[ *HwScsiFindAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff557300) SP が返す\_返す\_が見つかりました。

返されると、前に、 *HwScsiFindAdapter*レガシとプラグ アンド プレイの両方のミニポート ドライバーを設定する必要があります*再度*このセクションで説明します。 *再度*、プラグ アンド プレイ ドライバーとしてミニポート ドライバーが読み込まれるときに関係ありません*再度*システムは、必要な場合に、従来のドライバーのプラグ アンド プレイのミニポート ドライバーを実行できるように適切に設定する必要があります.

*HwScsiFindAdapter*設定する必要があります*再度*に**TRUE**をもう一度呼び出す必要があるかを示す*正確に同じポートを持つ\_構成\_情報がデバイスの新しい拡張機能、* 場合同じ I/O バス上の Hba のもう 1 つに接続する場合があります。

場合*HwScsiFindAdapter* HBA を見つけることができませんをサポートし、設定があります*再度*に**FALSE**戻って SP\_返す\_いない\_が見つかりました。 場合*HwScsiFindAdapter* HBA をサポートされているが、入力[**ポート\_構成\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff563900)が一貫性のない構成データ (無効ななど**もできます**または**BusInterruptLevel** EISA バス上)、設定があります*再度*に**FALSE**とSP が返す\_返す\_不良\_構成します。 PCI バス上の HBA の*HwScsiFindAdapter*システムによって提供される割り込み構成情報をそのまま使用する必要があります。

その設定に注意してください*再度*に**FALSE** sp の制御を返すと\_返す\_いない\_FOUND または SP\_返す\_悪い\_構成は、特定の I/O バスがで識別されることを示します、 **SystemIoBusNumber**入力ポートに\_構成\_についてには、ミニポート ドライバーをサポートする HBA がありません。 呼び出し元からシステム ポート ドライバーれない*HwScsiFindAdapter*もう一度更新ポート\_構成\_については、マシンに追加の I/O バスがある場合、HBA(s) を別の I/O バスをスキャンするには同じ**AdapterInterfaceType**します。

 

 




