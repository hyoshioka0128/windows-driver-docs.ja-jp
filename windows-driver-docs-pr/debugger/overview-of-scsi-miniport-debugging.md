---
title: SCSI ミニポートのデバッグの概要
description: SCSI ミニポートのデバッグの概要
ms.assetid: 9d05d416-aae4-453a-bdb0-2ac9148ad81d
keywords:
- SCSI ミニポート デバッグ, 概要
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81ab3db24688e5f23d30ed3cdfa443bfae90ed72
ms.sourcegitcommit: b25275c2662bfdbddd97718f47be9bd79e6f08df
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/13/2019
ms.locfileid: "67866521"
---
# <a name="overview-of-scsi-miniport-debugging"></a>SCSI ミニポートのデバッグの概要

## <a name="span-idoverviewofscsispanspan-idoverviewofscsispan-scsi-verification"></a><span id="overview_of_scsi"></span><span id="OVERVIEW_OF_SCSI"></span> SCSI の検証

小規模なコンピューター システム インターフェイス (SCSI) の拡張機能のデバッグは、2 つの拡張機能モジュールを参照してください。Scsikd.dll Minipkd.dll. これらのモジュールで最も重要な拡張機能コマンドの概要については、次を参照してください。 [SCSI ミニポート ドライバーのデバッグ用の拡張機能](extensions-for-debugging-scsi-miniport-drivers.md)します。 完全な一覧についてを参照してください。[ミニポート拡張機能の SCSI](scsi-miniport-extensions--scsikd-dll-and-minipkd-dll-.md)します。

SCSIkd.dll 拡張機能のコマンドは、任意のバージョンの Windows で使用できます。 Minipkd.dll 拡張機能のコマンドは、Windows XP および Windows の以降のバージョンでのみ使用できます。 Minipkd.dll でのコマンドでは、SCSI ポート ドライバーと連動するミニポート ドライバーに適用できるのみです。

SCSI ミニポート ドライバーをテストするには、Driver Verifier の SCSI 検証の機能を使用します。 Driver Verifier については、次を参照してください。 [Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier) Windows Driver Kit (WDK) ドキュメントです。
