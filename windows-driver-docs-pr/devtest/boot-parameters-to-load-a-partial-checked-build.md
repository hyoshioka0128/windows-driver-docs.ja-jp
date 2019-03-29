---
title: 部分チェック ビルドを読み込むためのブート パラメーター
description: 部分チェック ビルドを読み込むためのブート パラメーター
ms.assetid: 701a3258-d659-49a7-8e0d-52adc556a289
keywords:
- チェック ビルドの部分的なブート オプション WDK
- WDK のブート パラメーター
- ブート エントリ パラメーター WDK
- 読み込みの部分的なチェック ビルド WDK ブート オプション
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27993aaf78504ddf3ea490e98d52b0dea746b206
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570636"
---
#  <a name="boot-parameters-to-load-a-partial-checked-build"></a>部分チェック ビルドを読み込むためのブート パラメーター


## <span id="ddk_boot_parameters_to_load_a_partial_checked_build_tools"></span><span id="DDK_BOOT_PARAMETERS_TO_LOAD_A_PARTIAL_CHECKED_BUILD_TOOLS"></span>


A*チェック済みビルドの部分的な*チェック ビルド バージョンのカーネルと HAL およびオペレーティング システムの残りの部分の無料のビルドが含まれています。 詳細については、次を参照してください。[オペレーティング システムのチェックと HAL (For Windows Vista 以降) のみをインストールする](installing-just-the-checked-operating-system-and-hal--for-windows-vist.md)します。

### <a name="span-idconfiguringapartialcheckedbuildinwindowsvistaandlaterspanspan-idconfiguringapartialcheckedbuildinwindowsvistaandlaterspanconfiguring-a-partial-checked-build-in-windows"></a><span id="configuring_a_partial_checked_build_in_windows_vista_and_later"></span><span id="CONFIGURING_A_PARTIAL_CHECKED_BUILD_IN_WINDOWS_VISTA_AND_LATER"></span>Windows での部分的なチェック ビルドの構成

部分を構成するビルドの使用をチェック、 [ **BCDedit/set** ](https://msdn.microsoft.com/library/windows/hardware/ff542202)コマンドと**カーネル**と**hal**オプション。

次のコマンドは、チェックされているバージョンのカーネルとハードウェア アブストラクション レイヤー (HAL) を使用するブート エントリを構成します。

```
bcdedit /set {18b123cd-2bf6-11db-bfae-00e018e2b8db} kernel ntoskrnl.chk
```

```
bcdedit /set {18b123cd-2bf6-11db-bfae-00e018e2b8db} hal halacpi.chk
```

コマンドの結果を表示するには、次のように入力します。 **bcdedit/enum**します。 **/Enum**オプションには、すべてのブート エントリが一覧表示されます。 Checked HAL およびカーネルのバージョンを使用するように変更したブート エントリは、シリアル接続経由でのデバッグのカーネルでも設定されています。

```
## Windows Boot Loader
-------------------
identifier              {18b123cd-2bf6-11db-bfae-00e018e2b8db}
device                  partition=C:
path                    \Windows\system32\winload.exe
description             PartialCheckedBuild
locale                  en-US
inherit                 {bootloadersettings}
debugtype               serial
debugport               1
baudrate                115200
osdevice                partition=C:
systemroot              \Windows
kernel                  ntoskrnl.chk
hal                     halacpi.chk
resumeobject            {d7094401-2641-11db-baba-00e018e2b8db}
nx                      OptIn
debug                   Yes
```

 

 





