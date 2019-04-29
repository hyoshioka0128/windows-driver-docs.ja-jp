---
title: トレース コード内の NULL 文字列起こる
description: トレース コード内の NULL 文字列起こる
ms.assetid: a2226cbd-28cf-48eb-b129-5c4d12eb2564
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07a917abc0a5ebbf24b6cc6883ad523bee12ada7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386386"
---
# <a name="what-happens-to-null-strings-in-tracing-code"></a>トレース コード内の NULL 文字列に対する処理


既定では、このバージョンの Windows Driver Kit (WDK) でのトレーシング コンポーネントの検索の**NULL**関数に渡す引数の文字列。 その結果がありませんようにするのには、各引数を確認する**NULL**文字列から例外が発生します。

以前のバージョンの WDK、WPP\_確認\_の\_NULL\_文字列マクロは、この関数を実行します。 WDK のこのバージョンを使用して、カーネル モード ドライバーまたはユーザー モード アプリケーションをビルドする場合は、ソース コードからマクロを削除できます。

 

 





