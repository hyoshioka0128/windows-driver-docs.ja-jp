---
title: dbgerr002 無効なポインター
description: dbgerr002 無効なポインター
ms.assetid: d5f2404e-3e7d-4de2-a772-0d42169eb9ad
keywords:
- dbgerr002
- 無効なポインター (dbgerr002)
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97c0a79de5df862985213bb4c378fd011f8e917f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373450"
---
# <a name="dbgerr002-bad-pointer"></a>dbgerr002:Bad Pointer


## <span id="ddk_dbgerr002_dbg"></span><span id="DDK_DBGERR002_DBG"></span>


デバッガーのエラー **dbgerr002** 「無効なポインターです」というメッセージが表示されます。 このエラーは、シンボル ファイルの取得で問題を示します。

シンボル サーバーでは、インデックスを作成、ファイルがありますが、ファイルを検索する別の場所にリダイレクトされています。 ファイルではありませんアクセス可能なこの他の場所です。

この問題の 2 つの一般的な原因は次のとおりです。

-   パス、UNC パスでは、このサーバーを格納しているコンピューターは使用できません。

-   パスは、ディレクトリまたはファイルが削除されていることを示します。

SymStore を使用して、シンボル ストアが作成された場合は、file.ptr を調べることで、このファイルへの完全パスを検索できます。 詳細については、次を参照してください。[を使用して SymStore](symstore.md)します。

 

 





