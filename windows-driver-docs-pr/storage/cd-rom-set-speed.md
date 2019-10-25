---
title: CD-ROM 設定速度
description: CD-ROM 設定速度
ms.assetid: 25a46b23-f823-4fc7-a370-cab1c9418a94
keywords:
- CD-ROM ドライバー WDK ストレージ
- 記憶域 CD-ROM ドライバー WDK
- 電源管理 WDK CD-ROM
- WDK の高速 CD-ROM
- バッテリ電源 (WDK) cd-rom
- 再生速度 WDK CD-ROM
- スピンドル速度 WDK CD-ROM
- CD 速度の設定
- ストリーミングの設定
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88eccaddae806250717a2975a984c857185ca6d6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841626"
---
# <a name="cd-rom-set-speed"></a>CD-ROM 設定速度


多くの場合、CD-ROM ドライブで使用できる最適なスピンドル速度よりも速い速度で Cd をスピンすると便利です。 たとえば、ポータブルコンピューターでは、高速で高速に動作する CD-ROM ドライブを使用すると、バッテリが非常に高速に消費されます。 バッテリ電源を節約するために、CD-ROM ドライブを低速に設定することができます。

コンピューターによっては、CD-ROM ドライブを高速で動作させる必要がない場合があります。 たとえば、media center コンピューターの CD-ROM ドライブは、主に、の速度を必要としない、オーディオ再生などの操作を実行します。 再生中にスピンアップする CD-ROM ドライブ (再生中に16X など) は、1倍の速度が必要な場合は、ユーザーエクスペリエンスが悪いことにつながる大きなノイズが発生する可能性があります。

*SCSI 3 マルチメディアコマンド*(MMC) 仕様のバージョン2では、cd-rom の速度を設定するための2つのコマンド (cd 速度の設定とストリーミングの設定) が定義されています。 Windows Vista では、アプリケーションは CD-ROM クラスドライバーに対して、これら2つのコマンドのいずれかを発行するように指示することができます。これを行うには、 [ **\_CDROM\_\_SPEED**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_set_speed)要求をクラスドライバーに送信します。

[CD SPEED\_の設定] コマンドを CD-ROM デバイスに送信するには、呼び出し元は、 **CdromSetSpeed**の**RequestType**メンバー内の要求の種類として[ **\_速度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ns-ntddcdrm-_cdrom_set_speed)を指定します。これには、IOCTL\_CDROM\_設定\_速度を設定します。

SET STREAMING コマンドをデバイスに送信するために、呼び出し元は、 [ **\_ストリーミング\_設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ns-ntddcdrm-_cdrom_set_streaming)されている Cd-rom の**RequestType** **メンバー内の**要求の種類を指定しています。これは、IOCTL\_cdrom\_set に入力し\_低速.

アプリケーションで [CD SPEED の設定] コマンドを使用してスピンドル速度を変更した場合、メディアが変更されると、デバイスは自動的に既定の速度に戻ります。 アプリケーションが、SET STREAMING コマンドを使用してスピンドル速度を変更した場合、呼び出し元が CDROM\_SET\_STREAMING 構造体の**永続**メンバーに**FALSE**の値を指定していない限り、メディアの変更は速度に影響しません。

SET STREAMING 要求は、MMC に準拠しているデバイスでのみ機能します。 アプリケーションが MMC に準拠していないデバイスにこの要求を送信した場合、CD-ROM クラスドライバーは要求を失敗させます。

 

 




