---
title: CD-ROM ドライバーの概要
description: CD-ROM ドライバー
ms.assetid: 04b0a605-7816-4804-bfa8-39122a03ce16
keywords:
- CD-ROM ドライバー WDK ストレージ
- 記憶域 CD-ROM ドライバー WDK
- 記憶域ドライバー WDK、CD-ROM
- Ioctl WDK CD-ROM
ms.date: 12/15/2019
ms.localizationpriority: medium
ms.openlocfilehash: 9e1b455150c75c641ddd0a1666d0acbabc52f1ff
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606382"
---
# <a name="introduction-to-cd-rom-drivers"></a>CD-ROM ドライバーの概要

オペレーティングシステムによって CD-ROM デバイスが列挙されると、ネイティブの CD-ROM クラスドライバー (*Cdrom*) が読み込まれます。 このドライバーは、i/o 制御要求 (IOCTL) インターフェイスを公開します。 CD-ROM デバイスのドライバーのすべてのパブリック i/o 制御コードは、バッファー i/o を使用します。 そのため、これらの要求の入力データまたは出力データは、Irp-> AssociatedIrp にあります。 詳細については、「 [cd-rom i/o 制御コード](cd-rom-io-control-codes.md)」を参照してください。

CD-ROM デバイス用のクラスドライバーは、このセクションで説明されている追加のパブリック i/o 制御コードを処理します。 ストレージクラスドライバーの要件の詳細については、「[一般的なストレージ I/o 制御コード](general-storage-io-control-codes.md)」を参照してください。

次のトピックでは、CD-ROM クラスドライバーの IOCTL インターフェイスの主な機能の一部について説明します。

- [CD-ROM 専用アクセス](cd-rom-exclusive-access-mode.md)

- [CD-ROM の設定速度](cd-rom-set-speed.md)

- [CD-ROM のリアルタイムストリーミング](cd-rom-real-time-streaming-.md)

- [Acl とデバイススタック](acls-and-the-device-stack.md)
