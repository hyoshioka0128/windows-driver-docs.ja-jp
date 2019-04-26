---
title: CD-ROM ドライバー
description: CD-ROM ドライバー
ms.assetid: 04b0a605-7816-4804-bfa8-39122a03ce16
keywords:
- CD-ROM ドライバー WDK ストレージ
- CD-ROM のストレージ ドライバー WDK
- ストレージ ドライバー WDK、CD-ROM
- Ioctl WDK CD-ROM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 473785555fd63c98ea2cb111c4a0ffd503bffc68
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348468"
---
# <a name="cd-rom-drivers"></a>CD-ROM のドライバー

次のトピックでは、IOCTL インターフェイスの主要機能の一部について説明します。

[CD-ROM の排他アクセスを許可](cd-rom-exclusive-access-mode.md)

[CD-ROM セット速度](cd-rom-set-speed.md)

[CD-ROM のリアルタイムのストリーミング](cd-rom-real-time-streaming-.md)

[Acl とデバイス スタック](acls-and-the-device-stack.md)

オペレーティング システムでは、CD-ROM デバイスを列挙するネイティブ CD-ROM クラス ドライバーが読み込まれます (*Cdrom.sys*)。 このドライバーは、I/O 制御 (IOCTL) の要求インターフェイスを公開します。 パブリックのすべての I/O 制御コードが CD-ROM デバイスのドライバーでは、バッファー内の I/O を使用します。 その結果、入力または出力データは、これらの要求を Irp で]-> [AssociatedIrp.SystemBuffer します。 詳細については、次を参照してください[CD-ROM I/O 制御コード。](cd-rom-io-control-codes.md)

Cd-rom クラス ドライバーは処理追加パブリック I/O 制御コード、このセクションで説明したものとします。 記憶域クラス ドライバーの要件の詳細については、次を参照してください。[全般ストレージ I/O 制御コード](general-storage-io-control-codes.md)します。