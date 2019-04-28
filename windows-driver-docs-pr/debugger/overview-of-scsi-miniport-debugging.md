---
title: SCSI ミニポートのデバッグの概要
description: SCSI ミニポートのデバッグの概要
ms.assetid: 9d05d416-aae4-453a-bdb0-2ac9148ad81d
keywords:
- SCSI ミニポート デバッグ, 概要
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a08cb3c42c7fa770ff807e587dad123365951f4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366462"
---
# <a name="overview-of-scsi-miniport-debugging"></a>SCSI ミニポートのデバッグの概要


小規模なコンピューター システム インターフェイス (SCSI) の拡張機能のデバッグは、2 つの拡張機能モジュールを参照してください。Scsikd.dll Minipkd.dll. これらのモジュールで最も重要な拡張機能コマンドの概要については、次を参照してください。 [SCSI ミニポート ドライバーのデバッグ用の拡張機能](extensions-for-debugging-scsi-miniport-drivers.md)します。 完全な一覧についてを参照してください。[ミニポート拡張機能の SCSI](scsi-miniport-extensions--scsikd-dll-and-minipkd-dll-.md)します。

SCSIkd.dll 拡張機能のコマンドは、任意のバージョンの Windows で使用できます。 Minipkd.dll 拡張機能のコマンドは、Windows XP および Windows の以降のバージョンでのみ使用できます。 Minipkd.dll でのコマンドでは、SCSI ポート ドライバーと連動するミニポート ドライバーに適用できるのみです。

SCSI ミニポート ドライバーをテストするには、Driver Verifier の SCSI 検証の機能を使用します。 Driver Verifier については、次を参照してください。 [Driver Verifier](https://go.microsoft.com/fwlink/p/?linkid=120480) Windows Driver Kit (WDK) ドキュメントです。

 

 





