---
title: SymStore
description: SymStore
ms.assetid: acc7bf3a-62ea-4c93-843e-b81d4f71555f
keywords:
- SymStore の機能
- SymStore を使用して
- シンボル ストア、SymStore (symstore.exe)
ms.date: 03/27/2018
ms.localizationpriority: medium
ms.openlocfilehash: e22cad6b6b3bd3967a8b3148bbee3dcb73935653
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383002"
---
# <a name="symstore"></a>SymStore


## <span id="ddk_using_symstore_dbg"></span><span id="DDK_USING_SYMSTORE_DBG"></span>


SymStore (symstore.exe) は、シンボル ストアを作成するためのツールです。 これは、デバッグ ツールの Windows に含まれます。 詳細については、次を参照してください。[デバッグ ツールの Windows にダウンロード](https://docs.microsoft.com/windows-hardware/drivers/debugger/debugger-download-tools)します。

SymStore シンボル (.dbg または実行可能ファイル)、用のイメージまたは署名と有効期間 (.pdb ファイル) 用のサイズとタイムスタンプに基づくようにデバッガーにできるようにする形式でシンボルを格納します。 従来のシンボルのストレージ形式をシンボル ストアの利点は、すべてのシンボルの保存または同じサーバーで参照されているおよび事前知識がなくても、デバッガーによって取得されたをできることの製品、対応するシンボルが含まれています。

有効期間と同じシグネチャが含まれる各ため .pdb シンボル ファイル (たとえば、パブリックおよびプライベート バージョン) の複数のバージョンを同じサーバーに保存することはできないことに注意してください。

このセクションの内容:

[SymStore トランザクション](symstore-transactions.md)

[ファイル システムの参照とシンボル ファイル](file-system-references-and-symbol-files.md)

[SymStore 圧縮ファイル](symstore-compressed-files.md)

[ストレージ形式のシンボル](symbol-storage-format.md)

 

 





