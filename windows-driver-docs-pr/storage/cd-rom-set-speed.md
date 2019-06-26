---
title: CD-ROM 設定速度
description: CD-ROM 設定速度
ms.assetid: 25a46b23-f823-4fc7-a370-cab1c9418a94
keywords:
- CD-ROM ドライバー WDK ストレージ
- CD-ROM のストレージ ドライバー WDK
- 電源管理 WDK CD-ROM
- 速度の WDK CD-ROM
- バッテリ電源 WDK CD-ROM
- WDK の CD-ROM の再生速度
- スピンドル速度 WDK CD-ROM
- CD のスピードをセット
- ストリーミングの設定します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 527cbf2b02a93ad47a3f32ca76ec4d1dcf1ad615
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368341"
---
# <a name="cd-rom-set-speed"></a>CD-ROM 設定速度


多くの場合、Cd を CD-ROM ドライブができる最適なスピンドル速度よりも小さい速度で回転すると便利です。 たとえば、ポータブル コンピューターで高速で回転 CD-ROM ドライブ、バッテリーの消耗非常に高速です。 CD-ROM ドライブは、バッテリ電源を節約するために低速に設定できます。

一部のコンピューターでは、高速で動作を CD-ROM ドライブは必要ありません。 たとえば、media center コンピューターの CD-ROM ドライブでは、主に 1 X 上の速度を必要としないオーディオ再生をなどの操作を実行します。 CD-ROM ドライブに、スピン、たとえば、再生中、16 X 1 X だけの速度が必要なときに生成できる不適切なユーザー エクスペリエンスにつながる大きな音です。

バージョン 2、 *scsi-3 マルチ メディア コマンド*(MMC) の仕様には、CD-ROM の速度を設定するための 2 つのコマンドが定義されています。CD 速度の設定し、ストリーミングに設定します。 Windows Vista でアプリケーションは、送信することによってこれら 2 つのコマンドのいずれかの問題に CD-ROM クラス ドライバーを指示できます、 [ **IOCTL\_CDROM\_設定\_速度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_set_speed)クラスのドライバーに要求します。

呼び出し元の要求の種類の指定に CD-ROM デバイスを CD 速度の設定コマンドを送信する**CdromSetSpeed**で、 **RequestType**のメンバー [ **CDROM\_設定\_速度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ns-ntddcdrm-_cdrom_set_speed)、IOCTL への入力で\_CDROM\_設定\_速度。

呼び出し元の要求の種類の指定をデバイスにストリーミング設定のコマンドを送信する**CdromSetStreaming**で、 **RequestType**のメンバー [ **CDROM\_設定\_ストリーミング**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ns-ntddcdrm-_cdrom_set_streaming)、IOCTL への入力で\_CDROM\_設定\_速度。

アプリケーションでは、CD 速度の設定コマンドを使用して主軸速度を変更する場合、デバイスに自動的を返しますの既定の速度をメディアが変更されたときに。 アプリケーションでは、ストリーミング設定のコマンドを使用して主軸速度を変更する場合のメディアの変更には影響しません速度、呼び出し元の値を指定しない限り、 **FALSE**で、**持続**CD-ROM のメンバー\_設定\_ストリーミングの構造体。

ストリーミング設定要求は、MMC 準拠のデバイスでのみ機能します。 アプリケーションでは、MMC 準拠でないデバイスにこの要求を送信する場合、CD-ROM クラス ドライバーには、要求は失敗します。

 

 




