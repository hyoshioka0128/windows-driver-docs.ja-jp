---
title: カーネルモード ダンプ ファイルの作成
description: カーネルモード ダンプ ファイルの作成
ms.assetid: d3eb86b2-eba7-4ddb-90e9-0e26414436fb
keywords:
- ダンプ ファイル、カーネル モードのダンプ ファイルを作成します。
- ダンプ ファイル、NMI スイッチ
- NMI スイッチ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9198aa1b0d552078bc9058d402d5911073a9aa3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374454"
---
# <a name="creating-a-kernel-mode-dump-file"></a>カーネルモード ダンプ ファイルの作成


## <span id="ddk_creating_a_kernel_mode_dump_file_dbg"></span><span id="DDK_CREATING_A_KERNEL_MODE_DUMP_FILE_DBG"></span>


3 つの方法がカーネル モードのダンプ ファイルを作成できます。

1.  コントロール パネルで、ダンプ ファイルを有効にすることができ、単独で、システムがクラッシュします。

2.  コントロール パネルからダンプ ファイルを有効にし、クラッシュする、システムを強制できます。

3.  デバッガーを使用せず、システムのクラッシュ ダンプ ファイルを作成するのにことができます。

このセクションの内容:

[カーネル モードのダンプ ファイルを有効にします。](enabling-a-kernel-mode-dump-file.md)

[システムのクラッシュの強制](forcing-a-system-crash.md)

[せず、システムのクラッシュ ダンプ ファイルを作成します。](creating-a-dump-file-without-a-system-crash.md)

[カーネル モードのダンプ ファイルの作成を確認しています](verifying-the-creation-of-a-kernel-mode-dump-file.md)

### <a name="span-idusingannmiswitchspanspan-idusingannmiswitchspanusing-an-nmi-switch"></a><span id="using_an_nmi_switch"></span><span id="USING_AN_NMI_SWITCH"></span>NMI スイッチを使用

NMI スイッチを使用して、クラッシュ ダンプ ファイルを作成することもできます。 コンピューターにこのスイッチがあるかどうかを判断する、ハードウェアの製造元に問い合わせてください。

NMI スイッチの使用状況は、このドキュメントでは説明しません。

 

 





