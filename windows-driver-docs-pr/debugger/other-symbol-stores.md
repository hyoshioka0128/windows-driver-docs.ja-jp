---
title: その他のシンボル ストア
description: その他のシンボル ストア
ms.assetid: 65bb4291-c56a-4837-ac45-6751ebdbd579
keywords:
- シンボル ストア、独自のシンボル ストアの書き込み
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc2863c2ad0614c9b889712c39936e316724b618
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331260"
---
# <a name="other-symbol-stores"></a>その他のシンボル ストア


## <span id="ddk_using_other_symbol_stores_dbg"></span><span id="DDK_USING_OTHER_SYMBOL_STORES_DBG"></span>


SymStore を使用するのではなく、独自のシンボル ストア作成プログラムを記述することになります。

CSV 形式のテキスト ファイルにログに記録 SymStore トランザクションはすべて、データベース プログラムで使用する既存の SymStore ログ ファイルを利用できます。

プログラムが、Windows のツールをデバッグ パッケージで提供されることが推奨されます SymSrv を使用する場合も SymStore を使用します。 これら 2 つのプログラムの更新プログラムは、同時に、常に解放され、そのバージョンが一致常にそのためです。

 

 





