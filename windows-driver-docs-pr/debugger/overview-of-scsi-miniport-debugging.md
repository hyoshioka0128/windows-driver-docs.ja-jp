---
title: SCSI ミニポートのデバッグの概要
description: SCSI ミニポートのデバッグの概要
ms.assetid: 9d05d416-aae4-453a-bdb0-2ac9148ad81d
keywords:
- SCSI ミニポート デバッグ, 概要
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a08cb3c42c7fa770ff807e587dad123365951f4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581539"
---
# <a name="overview-of-scsi-miniport-debugging"></a>SCSI ミニポートのデバッグの概要


小規模なコンピューター システム インターフェイス (SCSI) の拡張機能のデバッグは、2 つの拡張機能モジュールを参照してください。Scsikd.dll Minipkd.dll. これらのモジュールで最も重要な拡張機能コマンドの概要については、[SCSI ミニポート ドライバーのデバッグ用の拡張機能](extensions-for-debugging-scsi-miniport-drivers.md)を参照してください。 完全な一覧についてを参照してください。[ミニポート拡張機能の SCSI](scsi-miniport-extensions--scsikd-dll-and-minipkd-dll-.md)します。

SCSIkd.dll 拡張機能のコマンドは、任意のバージョンの Windows で使用できます。 Minipkd.dll 拡張機能のコマンドは、Windows XP および Windows の以降のバージョンでのみ使用できます。 Minipkd.dll でのコマンドでは、SCSI ポート ドライバーと連動するミニポート ドライバーに適用できるのみです。

SCSI ミニポート ドライバーをテストするには、Driver Verifier の SCSI 検証の機能を使用します。 Driver Verifier については、[Driver Verifier](https://go.microsoft.com/fwlink/p/?linkid=120480) Windows Driver Kit (WDK) ドキュメントを参照してください。

 

 





