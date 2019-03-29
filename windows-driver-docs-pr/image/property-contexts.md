---
title: プロパティのコンテキスト
description: プロパティのコンテキスト
ms.assetid: da33848c-a9bc-40c7-ab1b-0ca056f3e06d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8523737fcc743e76ed27f53e5a7c72b2984f4af7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580044"
---
# <a name="property-contexts"></a>プロパティのコンテキスト





プロパティ コンテキストは、さまざまなプロパティがこれらのプロパティの検証中の対象を識別するために、ミニドライバーできる便利な手段を提供します。 プロパティ コンテキストを使用して、ミニドライバーをすばやく確認できます、識別されたプロパティのいずれかが変更されているかどうか。 ようにミニドライバーに WIA サービス ライブラリの関数のいずれかのプロパティのコンテキストが渡されます (たとえば、 [ **wiasGetChangedValueFloat**](https://msdn.microsoft.com/library/windows/hardware/ff549200))、アプリケーションは、かどうかを判断するコンテキストを使用します。プロパティの値を変更します。

WIA の検証方法は、アプリケーション プロパティが変更されると、依存関係プロパティも更新することです。 ただし、アプリケーションの依存プロパティも変更は場合、単にその新しい値が有効かどうかを判断する最上位レベルのプロパティを確認できます。 プロパティの検証に懸念を抱いている WIA サービス ライブラリ関数では、この原則を使用して、依存関係プロパティを更新する必要がありますと、ときに、有効性を確認する必要がありますだけを決定します。

プロパティのセットのコンテキストが保持、 [ **WIA\_プロパティ\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff552749)構造体は、3 つのメンバーが含まれています: プロパティでは、プロパティの数、プロパティの識別子 (Propid) の配列へのポインターとブール値の配列へのポインター。 並行して保持されますが、配列 (インデックス位置にあるプロパティ識別子を持つプロパティは、 *N*プロパティの識別子では配列に関連付けられたブール値配列内の同じインデックス位置にあるブール値)。

WIA サービス ライブラリ関数を呼び出すようにミニドライバー [ **wiasCreatePropContext**](https://msdn.microsoft.com/library/windows/hardware/ff549167)メモリを割り当てると、コンテキスト プロパティの値を入力します。 などの他の WIA サービス ライブラリ関数[ **wiasGetChangedValueFloat**](https://msdn.microsoft.com/library/windows/hardware/ff549200)プロパティの値をいつ更新するかを決定するプロパティのコンテキストを使用します。

 

 




