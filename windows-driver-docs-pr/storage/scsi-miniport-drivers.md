---
title: SCSI ミニポート ドライバー
description: SCSI ミニポート ドライバー
ms.assetid: d9268be8-a68d-4617-b323-349ce7c62f3f
keywords:
- SCSI ミニポート ドライバー WDK ストレージ
- ストレージ ミニポート ドライバー WDK、SCSI ミニポート ドライバー
- ミニポート ドライバー WDK ストレージ、SCSI ミニポート ドライバー
- SCSI ミニポート ドライバー WDK ストレージ、SCSI ミニポート ドライバーについて
- HBA WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a0e5523d18b6dbb500a41ffc48c6cc2c54a4924
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575140"
---
# <a name="scsi-miniport-drivers"></a>SCSI ミニポート ドライバー


## <span id="ddk_scsi_miniport_drivers_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_KG"></span>


このセクションには、次の情報が含まれています。

[SCSI ミニポート ドライバーのプラグ アンド プレイのサポート](supporting-plug-and-play-in-a-scsi-miniport-driver.md)

[プラグ アンド プレイ SCSI ミニポート ドライバーのレジストリ エントリ](registry-entries-for-plug-and-play-scsi-miniport-drivers.md)

[SCSI のミニポート ドライバーをブート ドライブの管理に関する制限事項](restrictions-on-scsi-miniport-drivers-that-manage-the-boot-drive.md)

[SCSI ミニポート ドライバーでのエラー処理](error-handling-in-scsi-miniport-drivers.md)

[必須およびオプションの SCSI ミニポート ドライバー ルーチン](required-and-optional-scsi-miniport-driver-routines.md)

NT ベースのオペレーティング システムのミニポート ドライバーを SCSI HBA 固有はオペレーティング システムに依存しません。 これは、システムが指定した SCSI ポート ドライバー ダイナミック リンク ライブラリ (DLL) は、ポートのドライバーだけの呼び出しでの各ミニポート ドライバー リンク自体 **ScsiPort * * * Xxx*システムとその HBA と通信するルーチン。 このような SCSI ミニポート ドライバーが Microsoft Win32 アプリケーションをサポートし、エクスポートも他の Microsoft オペレーティング システムで実行、**ScsiPort * * * Xxx*ルーチン。 詳細については、**ScsiPort * * * Xxx*ルーチンを参照してください[SCSI ポート ライブラリ ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff565375)します。

ある SCSI ミニポート ドライバーを呼び出すルーチン以外に注意してください。、**ScsiPort * * * Xxx* Microsoft オペレーティング システムの両方の環境で実行することはできません。 のみ、システム提供の NT ベースのオペレーティング システムを含む、Microsoft Windows のシステム間で移植可能なままに SCSI ミニポート ドライバーが呼び出す必要があります **ScsiPort * * * Xxx*します。

SCSI ミニポート ドライバーは、プラグ アンド プレイ ドライバーまたはリソースの再配布や電源管理などのプラグ アンド プレイ操作に参加していないレガシ ドライバーとして実行できます。 プラグ アンド プレイと従来のミニポート ドライバーの主な違いは、初期化ルーチンを呼び出すと Microsoft Windows NT 4.0、ミニポート ドライバーに適用されたは使用されませんが特定の制限の適用順序です。

 

 




