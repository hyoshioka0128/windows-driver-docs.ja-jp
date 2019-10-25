---
title: ビデオミニポートドライバーのテレビコネクタとコピー防止機能
description: テレビ ミニポート ドライバーでのテレビ コネクタおよびコピー防止サポート
ms.assetid: 7d7d44b5-3248-4bee-bc4d-e02fd3c606a7
keywords:
- ビデオミニポートドライバー WDK Windows 2000、TV コネクタ
- ビデオミニポートドライバー WDK Windows 2000、コピー保護サポート
- TV コネクタ WDK ビデオミニポート
- コピー防止 WDK ビデオミニポート
- IOCTL_VIDEO_HANDLE_VIDEOPARAMETERS
- コピー防止 WDK ビデオミニポート、コピー防止サポートについて
- ハードウェア WDK コピー防止
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 419d42bd08e3625da76dbea68fdd3d88f47dd984
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825417"
---
# <a name="tv-connector-and-copy-protection-support-in-video-miniport-drivers"></a>テレビ ミニポート ドライバーでのテレビ コネクタおよびコピー防止サポート

TV コネクタがあるアダプターのビデオミニポートドライバーは、VIDEOPARAMETERS I/o 制御コード\_処理するために、 [**IOCTL\_video\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_handle_videoparameters)で[**vrps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_request_packet)を処理する必要があります。 この IOCTL はミニポートドライバーに送信され、テレビコネクタの機能と現在の設定を照会するか、またはテレビコネクタとコピー防止ハードウェアの機能を設定します。 ミニポートドライバーは、VRP の**InputBuffer**で渡される[**VIDEOPARAMETERS**](https://docs.microsoft.com/windows/desktop/api/tvout/ns-tvout-_videoparameters)構造体の**dwcommand**フィールドをチェックすることによって、実行するアクションを決定します。 ミニポートドライバーがこの VRP を処理しない場合、システムは Rovi (旧称 Macrovision) で保護されている Dvd を再生できません。

**Dwcommand**が VP\_COMMAND\_GET に設定されていて、デバイスがテレビ出力をサポートして*いない*場合、ミニポートドライバーは VRP の**statusblock**の**Status**メンバーに\_エラーを返しません。 また、VRP の**Statusblock**の**情報**メンバーを VIDEOPARAMETERS 構造体のサイズ (バイト単位) に設定する必要があります。 この場合は、 **dwFlags**をゼロに設定し、 **dwTVStandard**を VP\_TV\_STANDARD\_win\_vga に設定し、 **Dwavailability AB VSTANDARD**を VP\_TV\_standard\_win\_VGA に設定します。

**Dwcommand**が VP\_COMMAND\_GET に設定されていて *、デバイスが*テレビをサポートしている場合、VIDEOPARAMETERS 構造体では、次のように、 **dwFlags**メンバーとの適切なフラグを設定することによってこれを示す必要があります。設定フラグに対応する他の構造体メンバーに値を代入します。

次のセクションでは、テレビコネクタを持つデバイスのミニポートドライバーの実装の詳細について説明します。

[テレビコネクタとコピー防止ハードウェアのクエリ](querying-tv-connector-and-copy-protection-hardware.md)

[コピー防止ハードウェアの設定](setting-copy-protection-hardware.md)

 

 





