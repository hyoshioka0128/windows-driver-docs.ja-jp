---
title: INF HardwareId ディレクティブ
description: 新しいハードウェアの検出ウィザードとハードウェアの更新ウィザードは、Autorun.inf ファイルの [DeviceInstall] セクションで INF HardwareId ディレクティブをサポートしています。
ms.assetid: aceb4db2-ae00-47f3-994a-49541437e260
keywords:
- INF HardwareId ディレクティブデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF HardwareId Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4fab109e239f4e0dcd13858317011e27f72a1f8b
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223288"
---
# <a name="inf-hardwareid-directive"></a>INF HardwareId ディレクティブ


**注**   **HardwareId**ディレクティブは、*自動実行 .inf*ファイル内でのみサポートされています。 このディレクティブは、PnP デバイスのインストールに使用される INF ファイル内では使用しないでください。

 

Windows Vista 以降では、新しいハードウェアの検出ウィザードとハードウェア更新ウィザードが、 *autorun.inf*ファイルの** \[DeviceInstall\] **セクションにある inf **HardwareId**ディレクティブをサポートしています。 *Autorun.inf*の作成者は、これらの**HardwareId**ディレクティブを使用して、自動実行対応アプリケーションによってドライバーが提供およびインストールされるデバイスのプラグアンドプレイ (PnP) ハードウェア識別子 (IDs) を指定できます。

```inf
[DeviceInstall] 
 
HardwareId="pnp-hardware-id"
...
```

## <a name="entries"></a>エントリ


<a href="" id="-pnp-hardware-id-"></a>"*pnp-ハードウェア id*"  
この値は、PnP デバイスのハードウェア ID を指定します。 ハードウェア ID は二重引用符 (") で囲む必要があります。

ハードウェア ID は、PCI\\VEN_1234&DEV_1234 などの非常に汎用的な場合もあれば、pci\\VEN_1234&DEV_1234&SUBSYS_12345678&REV_01 のような非常に固有のものもあります。

HardwareId ディレクティブごとに指定できる PnP ハードウェア ID は1つだけです。 複数のハードウェア Id を指定するには、複数の HardwareId ディレクティブを1行に1つずつ使用します。

<a name="remarks"></a>解説
-------

ハードウェアの[初回インストール](hardware-first-installation.md)時には、そのデバイスのドライバーをインストールする前に、ユーザーがハードウェアデバイスをインストールします。 この場合は、新しいハードウェアの検出ウィザードによって、ユーザーに配布メディアの入力が求められます。

配布メディアに自動実行が有効な*デバイスインストールアプリケーション*がある場合、ウィザードによって自動実行の *.inf*ファイルが解析され、インストールされているデバイスに一致する**HardwareId**ディレクティブエントリが検索されます。 デバイスに一致する**HardwareId**ディレクティブが検出された場合、ウィザードは自動実行対応アプリケーションを起動します。これにより、ウィザードの代わりにドライバーとデバイス固有のアプリケーションがインストールされます。

新しいハードウェアの検出ウィザードでは、アプリケーションによってデバイスのドライバーがインストールされているかどうかは判断されません。 この場合、アプリケーションはデバイス用のドライバーをインストールする必要があります。 インストールされているデバイスを識別する**HardwareId**ディレクティブが自動実行の *.inf*ファイルに含まれていない場合、ウィザードはアプリケーションを起動せず、デバイスのインストールを続行します。

*自動実行 .inf*ファイルの** \[DeviceInstall\] **セクションには複数の**HardwareId**ディレクティブが存在する場合がありますが、各ディレクティブには一意の PnP ハードウェア ID を指定する必要があります。

 

 





