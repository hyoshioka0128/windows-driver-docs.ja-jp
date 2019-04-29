---
title: OpenGL との相互運用性の無効化
description: OpenGL との相互運用性の無効化
ms.assetid: 2b684cda-2137-4395-b2ee-beee8614e4c1
keywords:
- INF ファイル WDK の表示、相互運用性
- WDK の表示の相互運用性
- OpenGL WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: df93c9bd39b6f7d8ee413b9528ae7453ed4510c5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63393043"
---
# <a name="disabling-interoperability-with-opengl"></a>OpenGL との相互運用性の無効化


OpenGL インストール可能なクライアント ドライバー (ICDs) で可能な相互運用性の問題をマイクロソフトの Direct3D ディスプレイ ドライバーが公開されるしないことを確認するには、INF の追加レジストリ セクションで、次のエントリを設定する必要があります。

```inf
[Xxx_SoftwareDeviceSettings]
...
HKR,, CapabilityOverride,    %REG_DWORD%, 0x8
```

 

 





