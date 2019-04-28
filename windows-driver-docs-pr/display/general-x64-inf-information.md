---
title: 一般的な x64 INF 情報
description: 一般的な x64 INF 情報
ms.assetid: a1a96e8f-74d3-403d-994a-b21436d166d2
keywords:
- INF ファイル WDK の表示、64 ビット
- 64 ビットの WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d6460ae99f513dcf006f491efa871019739276a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366332"
---
# <a name="general-x64-inf-information"></a>一般的な x64 INF 情報


X64 に固有の次の情報は、64 ビット Windows Vista 以降を実行しているディスプレイ ドライバーをロードする INF ファイルに必要です。

```inf
[DestinationDirs]
DefaultDestDir  = 11
R200.Miniport   = 12  ; drivers
R200.Display    = 11  ; system32
R200.DispWow  = 10, SysWow64 ; x64-specific

[Manufacturer]
%ATI% = ATI.Mfg, NTamd64 ; Ntamd64 is x64-specific

[ATI.Mfg.NTamd64] ; Ntamd64 is x64-specific

[R200_RV200]
FeatureScore=F8
CopyFiles=R200.Miniport, R200.Display, R200.DispWow ; R200.DispWow is x64-specific
AddReg = R200_SoftwareDeviceSettings
AddReg = R200_RV200_SoftwareDeviceSettings
DelReg = R200_RemoveDeviceSettings

; File sections
;

[r200.Miniport]
r200.sys

[r200.Display]
r200umd.dll,,,0x00004000  ; COPYFLG_IN_USE_TRY_RENAME

; The following [R200.DispWow] section is x64-specific

[R200.DispWow]
r2umd32.dll,,,0x00004000  ; COPYFLG_IN_USE_TRY_RENAME
```