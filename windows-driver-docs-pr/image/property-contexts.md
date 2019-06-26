---
title: プロパティのコンテキスト
description: プロパティのコンテキスト
ms.assetid: da33848c-a9bc-40c7-ab1b-0ca056f3e06d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fab194f3357ec9d722aba61bd1f337ff66c423e3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374315"
---
# <a name="property-contexts"></a>プロパティのコンテキスト





プロパティ コンテキストは、さまざまなプロパティがこれらのプロパティの検証中の対象を識別するために、ミニドライバーできる便利な手段を提供します。 プロパティ コンテキストを使用して、ミニドライバーをすばやく確認できます、識別されたプロパティのいずれかが変更されているかどうか。 ようにミニドライバーに WIA サービス ライブラリの関数のいずれかのプロパティのコンテキストが渡されます (たとえば、 [ **wiasGetChangedValueFloat**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetchangedvaluefloat))、アプリケーションは、かどうかを判断するコンテキストを使用します。プロパティの値を変更します。

WIA の検証方法は、アプリケーション プロパティが変更されると、依存関係プロパティも更新することです。 ただし、アプリケーションの依存プロパティも変更は場合、単にその新しい値が有効かどうかを判断する最上位レベルのプロパティを確認できます。 プロパティの検証に懸念を抱いている WIA サービス ライブラリ関数では、この原則を使用して、依存関係プロパティを更新する必要がありますと、ときに、有効性を確認する必要がありますだけを決定します。

プロパティのセットのコンテキストが保持、 [ **WIA\_プロパティ\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/ns-wiamindr_lh-_wia_property_context)構造体は、3 つのメンバーが含まれています: プロパティでは、プロパティの数、プロパティの識別子 (Propid) の配列へのポインターとブール値の配列へのポインター。 並行して保持されますが、配列 (インデックス位置にあるプロパティ識別子を持つプロパティは、 *N*プロパティの識別子では配列に関連付けられたブール値配列内の同じインデックス位置にあるブール値)。

WIA サービス ライブラリ関数を呼び出すようにミニドライバー [ **wiasCreatePropContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiascreatepropcontext)メモリを割り当てると、コンテキスト プロパティの値を入力します。 などの他の WIA サービス ライブラリ関数[ **wiasGetChangedValueFloat**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetchangedvaluefloat)プロパティの値をいつ更新するかを決定するプロパティのコンテキストを使用します。

 

 




