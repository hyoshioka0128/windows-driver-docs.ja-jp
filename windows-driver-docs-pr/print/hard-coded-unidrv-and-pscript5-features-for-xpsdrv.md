---
title: XPSDrv 向けにハード コーディングされた UniDrv および PScript5 機能
description: XPSDrv 向けにハード コーディングされた UniDrv および PScript5 機能
ms.assetid: d2922bc4-83d7-40da-adee-15c0810f2321
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d9ed9ac627a98959a5d91e35afd9e3ded26c6f9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571071"
---
# <a name="hard-coded-unidrv-and-pscript5-features-for-xpsdrv"></a>XPSDrv 向けにハード コーディングされた UniDrv および PScript5 機能


XPSDrv モードで実行されている、すべての Unidrv または PScript5 ハード コーディングされた機能は無効になります。 Unidrv/PScript5 ハード コーディングされた機能は、ドライバーの GPD/PPD ファイルが指定されていない機能です。

次のようには、ハード コーディングされた機能が無効になります。

-   機能は、Unidrv または PScript5 の中核となるドライバーの任意のユーザー インターフェイス (UI) には表示されません。

-   Microsoft Win32 DeviceCapabilities API、Unidrv または PScript5 ドライバーの**DrvDeviceCapabilities**関数は、ハード コーディングされた機能を報告しません。

-   PrintCapabilities XML では、ハード コーディングされた機能は含まれません。

-   PrintTickets を既定では、ハード コーディングされた機能の設定は含まれません。

さらに、このセクションの残りのトピックでは、ハード コーディングされた機能を無効にする前の領域で Unidrv PScript5 ベース XPSDrv の変更について説明します。

 

 




