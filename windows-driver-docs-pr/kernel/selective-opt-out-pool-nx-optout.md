---
title: 選択的オプトアウト POOL_NX_OPTOUT
description: メカニズム一連のドライバーのソース ファイルのオプトイン プールのデータ実行 (NX) のいずれかをグローバルに有効にして、POOL_NX_OPTOUT で 1 つまたは複数の選択したソース ファイルをこのオプトイン メカニズムをオーバーライドすることができます。
ms.assetid: 15AA7CFA-5BEC-4E45-B222-0DE2D620E099
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 90f09acf6967dc08997ece19f0b37011f8195188
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342681"
---
# <a name="selective-opt-out-poolnxoptout"></a>選択的オプトアウト: プール\_NX\_OPTOUT


メカニズム一連のドライバーのソース ファイルのオプトイン プールのデータ (NX) の実行の 1 つをグローバルに有効化してプールに 1 つまたは複数の選択したソース ファイルをこのオプトイン メカニズムをオーバーライドして\_NX\_OPTOUT します。 これにより、実行可能ファイルの非ページ メモリの使用継続を選択したソース ファイルができます。 プールを使用する\_NX\_OPTOUT オプトアウト メカニズムのいずれかのプールを\_NX\_OPTIN またはプール\_NX\_OPTIN\_自動オプトイン メカニズム。 詳細については、次を参照してください。[プール オプトイン メカニズムに NX](nx-pool-opt-in-mechanisms.md)します。

プールを使用する\_NX\_出力のオプトアウト メカニズムを選択したソース ファイルでオプトイン メカニズムをオーバーライドして、このファイルに次の定義を追加します。

`#define POOL_NX_OPTOUT 1`

この定義がのインスタンスを選択したファイルのグローバル オプトイン設定が上書きされますできず、 **NonPagedPool**の置換の定数の名前。 この定義の最初のインスタンスの前に、ファイルに挿入**NonPagedPool**ファイル。

プールを使用する代わりに\_NX\_OPTOUT のオプトアウト メカニズムをソース ファイルでは、各インスタンスを明示的に置換する**NonPagedPool**ファイルで**NonPagedPoolExecute**.

 

 




