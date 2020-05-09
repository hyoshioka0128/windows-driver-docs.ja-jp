---
title: 部分チェック ビルドを読み込むためのブート パラメーター
description: 部分チェック ビルドを読み込むためのブート パラメーター
ms.assetid: 701a3258-d659-49a7-8e0d-52adc556a289
keywords:
- 部分的にチェックされたビルドブートオプション WDK
- ブートパラメーター WDK
- ブートエントリパラメーター WDK
- 部分チェックビルドの WDK ブートオプションを読み込んでいます
ms.date: 05/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: fa6ca83044bbf0b80cca960f693dc680b358eb81
ms.sourcegitcommit: 076f9cd83313f6d8ab5688340f05bde7e8fbb8ee
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/09/2020
ms.locfileid: "82999027"
---
#  <a name="boot-parameters-to-load-a-partial-checked-build"></a>部分チェック ビルドを読み込むためのブート パラメーター

## <span id="ddk_boot_parameters_to_load_a_partial_checked_build_tools"></span><span id="DDK_BOOT_PARAMETERS_TO_LOAD_A_PARTIAL_CHECKED_BUILD_TOOLS"></span>

*部分チェック*されたビルドには、カーネルと HAL のチェックを行ったビルドバージョンと、オペレーティングシステムの残りの部分の無料ビルドが含まれています。 詳細については、「チェックされ[たオペレーティングシステムと HAL だけをインストールする (Windows Vista 以降)](installing-just-the-checked-operating-system-and-hal--for-windows-vist.md)」を参照してください。

> [!NOTE]
> チェックを行ったビルドは、Windows 10 バージョン1803より前の古いバージョンの Windows で使用できました。
> ドライバーの検証ツールや GFlags などのツールを使用してドライバーコードを確認します。


### <a name="span-idconfiguring_a_partial_checked_build_in_windows_vista_and_laterspanspan-idconfiguring_a_partial_checked_build_in_windows_vista_and_laterspanconfiguring-a-partial-checked-build-in-windows"></a><span id="configuring_a_partial_checked_build_in_windows_vista_and_later"></span><span id="CONFIGURING_A_PARTIAL_CHECKED_BUILD_IN_WINDOWS_VISTA_AND_LATER"></span>Windows での部分チェックされたビルドの構成

部分チェックされたビルドを構成するには、 [**BCDedit/set**](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--set)コマンドおよび**カーネル**と**hal**のオプションを使用します。

次のコマンドは、チェックされたバージョンのカーネルとハードウェアアブストラクションレイヤー (HAL) を使用するようにブートエントリを構成します。

```console
bcdedit /set {18b123cd-2bf6-11db-bfae-00e018e2b8db} kernel ntoskrnl.chk
```

```console
bcdedit /set {18b123cd-2bf6-11db-bfae-00e018e2b8db} hal halacpi.chk
```

コマンドの結果を表示するには、「 **bcdedit/enum**」と入力します。 **/Enum**オプションを指定すると、すべてのブートエントリが一覧表示されます。 カーネルと HAL のチェックされたバージョンを使用するように変更されたブートエントリも、シリアル接続を介したカーネルデバッグ用に構成されています。

```console
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
