---
title: KD でのコール スタックの表示
description: KD のいずれかの k (Display Stack Backtrace) コマンドを入力して、呼び出し履歴を表示できます。
ms.assetid: 81F5D9EA-48CE-4F29-B74E-282824E690F6
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6793772ad6c0ff6ea65eb5e2d0f2322a491473ec
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325910"
---
# <a name="viewing-the-call-stack-in-kd"></a>KD でのコール スタックの表示


呼び出し履歴は、プログラム カウンターの現在の場所が原因となった関数呼び出しのチェーンです。 呼び出し履歴の最上位の関数は、現在の関数で、次の関数は、現在の関数を呼び出した関数、という具合です。 表示される呼び出し履歴は、レジスタのコンテキストを変更しない限り、現在のプログラム カウンターに基づいています。 レジスタのコンテキストを変更する方法の詳細については、次を参照してください。[変更コンテキスト](changing-contexts.md)します。

KD のいずれかを入力して、呼び出し履歴を表示できます、 [ **k (Display Stack Backtrace)** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)コマンド。

 

 





