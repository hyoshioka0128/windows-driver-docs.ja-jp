---
title: OpenGL と相互運用性を無効にします。
description: OpenGL と相互運用性を無効にします。
ms.assetid: 2b684cda-2137-4395-b2ee-beee8614e4c1
keywords:
- INF ファイル WDK の表示、相互運用性
- WDK の表示の相互運用性
- OpenGL WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: df93c9bd39b6f7d8ee413b9528ae7453ed4510c5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530200"
---
# <a name="disabling-interoperability-with-opengl"></a>OpenGL と相互運用性を無効にします。


OpenGL インストール可能なクライアント ドライバー (ICDs) で可能な相互運用性の問題をマイクロソフトの Direct3D ディスプレイ ドライバーが公開されるしないことを確認するには、INF の追加レジストリ セクションで、次のエントリを設定する必要があります。

```inf
[Xxx_SoftwareDeviceSettings]
...
HKR,, CapabilityOverride,    %REG_DWORD%, 0x8
```

 

 





