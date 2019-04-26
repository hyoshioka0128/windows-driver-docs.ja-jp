---
title: INF HardwareId ディレクティブ
description: 新しいハードウェアの検出ウィザードとハードウェアの更新ウィザードは、Autorun.inf ファイルの [DeviceInstall] セクションでは INF HardwareId ディレクティブをサポートします。
ms.assetid: aceb4db2-ae00-47f3-994a-49541437e260
keywords:
- INF HardwareId ディレクティブ デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF HardwareId Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5a364030ddade721a392b3a7b3b513efcf03e59
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346113"
---
# <a name="inf-hardwareid-directive"></a>INF HardwareId ディレクティブ


**注**  、 **HardwareId**ディレクティブが内でのみサポートされている、 *Autorun.inf*ファイル。 PnP デバイスのインストールに使用される INF ファイル内は、このディレクティブを使用する必要があります。

 

Windows Vista 以降、新しいハードウェアの検出ウィザードとハードウェアの更新ウィザード サポート INF **HardwareId**ディレクティブ、 **\[DeviceInstall\]** のセクション*Autorun.inf*ファイル。 作成者*Autorun.inf*これらを使用して**HardwareId**自動実行が有効なアプリケーションを提供するデバイスのプラグ アンド プレイ (PnP) ハードウェア識別子 (Id) を指定するディレクティブとドライバーをインストールします。

```ini
[DeviceInstall] 
 
HardwareId="pnp-hardware-id"
...
```

## <a name="entries"></a>エントリ


<a href="" id="-pnp-hardware-id-"></a>"*pnp-hardware-id*"  
この値は PnP デバイスのハードウェア ID を指定します ハードウェア ID を二重引用符 (") で囲む必要があります。

ハードウェア ID はかなり汎用的で、PCI など、\\VEN_1234 & DEV_1234、PCI など、非常に固有または\\VEN_1234 & DEV_1234 & SUBSYS_12345678 REV_01 します。

HardwareId ディレクティブごと、1 つだけのプラグ アンド プレイ ハードウェア ID を指定できます。 複数のハードウェア Id を指定するには、複数の HardwareId ディレクティブの行ごとに 1 つを使用します。

<a name="remarks"></a>注釈
-------

中に、[ハードウェア最初インストール](hardware-first-installation.md)ユーザーがそのデバイスのドライバーをインストールする前に、ハードウェア デバイスをインストールします。 この場合、新しいハードウェアの検出ウィザードには、配布メディアのユーザー メッセージが表示されます。

配布中に自動実行が有効*デバイス インストール アプリケーション*、ウィザードによって解析され、 *Autorun.inf*ファイルを探して、 **HardwareId**ディレクティブインストールされているデバイスに一致するエントリ。 ウィザードが検出された場合、 **HardwareId**デバイスに一致するディレクティブ、ウィザードは、ドライバーと、ウィザードではなくデバイスに固有のアプリケーションをインストール、自動実行が有効なアプリケーションを呼び出します。

新しいハードウェアの検出ウィザードは、アプリケーションがデバイスのドライバーをインストールするかどうかを決定できません。 この場合、アプリケーションは、デバイスのドライバーをインストールする必要があります。 場合、 *Autorun.inf*ファイルは含まれません、 **HardwareId**ディレクティブにインストールされているデバイス、ウィザードは、アプリケーションが起動しないと、デバイスのインストールを続行します。

複数存在する可能性がありますが**HardwareId**ディレクティブ内で、 **\[DeviceInstall\]** のセクション、 *Autorun.inf*それぞれのファイルディレクティブは、一意のプラグ アンド プレイ ハードウェア ID を指定する必要があります。

 

 





