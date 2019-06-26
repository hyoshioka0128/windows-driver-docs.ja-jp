---
title: ブート パラメーターの変更
description: ブート パラメーターの変更
ms.assetid: e835e1e9-ad80-462b-b55f-2fa0e55009a5
keywords:
- ブート エントリ パラメーター WDK
- WDK のブート パラメーター
- ブート オプション WDK、ブート パラメーター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 519cac2938ab247961affcbc8f3d1339cad13fd6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371614"
---
# <a name="changing-boot-parameters"></a>ブート パラメーターの変更

有効にし、デバッグなど、オペレーティング システムのブートに関連する機能を構成するには、ブート パラメーターをオペレーティング システムのブート エントリを追加する必要があります。

Windows を実行するシステム上のブート パラメーターを変更するには、BCDEdit を使用することができます。

## <a name="span-idusingbcdeditspanspan-idusingbcdeditspanusing-bcdedit"></a><span id="using_bcdedit"></span><span id="USING_BCDEDIT"></span>BCDEdit を使用してください。

にブート エントリを、ブート構成パラメーターを追加するなど、グローバル設定を変更する BCDEdit のブート エントリのオプションを使用して、 **/ems**、 **/debug**、 **/dbgsettings**、または設定します。個々 のパラメーターを使用して、 [ **BCDEdit/set** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--set)オプション。 コマンド プロンプトで、BCDEdit のオプションの完全な一覧については、入力**BCDEdit/でしょうか。** または**BCDEdit/でしょうか。** &lt;コマンド&gt;特定のコマンドに関するヘルプを検索します。

たとえば、次のコマンドは、指定されたブート エントリの PAE を有効。 にします。

```
bcdedit /set {802d5e32-0784-11da-bd33-000476eba25f} pae forceenable
```

カーネル デバッガーをオンまたはオフを使用して、 **/debug**次の構文とオプション。

```
bcdedit /debug <ID> [on | off]
```

&lt;ID&gt;ブート エントリに関連付けられた GUID です。 指定しない場合、 &lt;ID&gt;のコマンドは、現在アクティブになっているオペレーティング システムを変更します。 次のコマンドは、DebugEntry と呼ばれる、ブート エントリのカーネル デバッガーを有効にします。

```
bcdedit /debug {49916baf-0e08-11db-9af4-000bdbd316a0} on
```

現在のブート エントリを表示するには、次のように入力します。 **bcdedit**コマンド プロンプトでします。 DebugEntry のブート エントリは、カーネル デバッガーがオンになっていることを示しています。

```
## Windows Boot Loader
-------------------
identifier              {49916baf-0e08-11db-9af4-000bdbd316a0}
device                  partition=C:
path                    \Windows\system32\winload.exe
description             DebugEntry
locale                  en-US
inherit                 {bootloadersettings}
osdevice                partition=C:
systemroot              \Windows
resumeobject            {3e3a9f69-024a-11db-b5fc-a50a1ad8a70e}
nx                      OptIn
pae                     ForceEnable
debug                   Yes
```
