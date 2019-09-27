---
title: グローバル フラグとイメージ ファイルの 13 の例の一覧
description: グローバル フラグとイメージ ファイルの 13 の例の一覧
ms.assetid: 1b1285d5-ed73-49c4-a123-de9cbdb3090c
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 996f85db746fcc628ea6beb3de3b9249ee8e97bb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347767"
---
# <a name="example-13-listing-image-files-with-global-flags"></a>例 13:グローバル フラグを使用してイメージ ファイルを一覧表示する


## <span id="ddk_example_13___listing_image_files_with_global_flags_dtools"></span><span id="DDK_EXAMPLE_13___LISTING_IMAGE_FILES_WITH_GLOBAL_FLAGS_DTOOLS"></span>


GFlags、特定のイメージ ファイルに設定されているフラグが表示されますが、設定フラグが設定されているすべてのイメージ ファイルは表示されません。

イメージのファイルを Windows はフラグを格納、 **GlobalFlag**次のレジストリ パスにイメージ ファイルの名前が付いたレジストリ サブキーのレジストリ エントリ**HKEY\_LOCAL\_MACHINE\\ SOFTWARE\\ Microsoft\\ Windows NT\\ CurrentVersion\\ Image File Execution Options\\*ImageFileName*\\GlobalFlag** します。

どのイメージを決定するには、は、ファイルには、Reg (reg.exe)、Windows Server 2003 に含まれるツールを使用して、フラグが設定されています。

次の Reg**クエリ**コマンドを検索、 **GlobalFlag**レジストリ エントリで指定されたレジストリ パス。 **-V**パラメーターを指定します、 **GlobalFlag**レジストリ エントリ。 **/S**パラメーターは、再帰的に検索します。

```console
reg query "HKLM\Software\Microsoft\Windows NT\CurrentVersion\Image File Execution Options" /v GlobalFlag /s
```

Reg 応答のすべてのインスタンスを表示、 **GlobalFlag**レジストリ エントリのパスとエントリの値。

```console
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\notepad.exe
    GlobalFlag    REG_SZ    0x00001000

HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\photohse.EXE
    GlobalFlag    REG_SZ    0x00200000

HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\printhse.EXE
    GlobalFlag    REG_SZ    0x00200000
```

**ヒント:**   型、 **Reg** 、メモ帳にコマンドの後、imageflags.bat として、ファイルを保存します。 その後、フラグが設定されているイメージ ファイルを検索する入力**ImageFlags**します。

 

 

 





