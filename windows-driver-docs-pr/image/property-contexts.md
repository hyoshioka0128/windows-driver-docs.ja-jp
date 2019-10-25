---
title: プロパティのコンテキスト
description: プロパティのコンテキスト
ms.assetid: da33848c-a9bc-40c7-ab1b-0ca056f3e06d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61cc8517f4c9131e29b7486fa6a23cb8dca4557e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840772"
---
# <a name="property-contexts"></a>プロパティのコンテキスト





プロパティコンテキストは、これらのプロパティの検証中に必要な多数のプロパティをミニドライバーが識別できる便利な方法を提供します。 プロパティコンテキストを使用すると、ミニドライバーは、識別されたプロパティのいずれかが変更されているかどうかをすばやく判断できます。 次に、ミニドライバーは、プロパティコンテキストを、アプリケーションがプロパティの値を変更しているかどうかを判断するためにコンテキストを使用[**する、WIA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchangedvaluefloat)サービスライブラリ関数のいずれかに渡します。

WIA の検証方法では、アプリケーションがプロパティを変更するときに、依存するプロパティも更新する必要があります。 ただし、アプリケーションで依存プロパティも変更されている場合は、トップレベルのプロパティを確認して、新しい値が有効かどうかを確認するだけです。 プロパティの検証に関係する WIA サービスライブラリ関数は、この原則を使用して、依存プロパティを更新するタイミングと、有効性を確認するだけのタイミングを決定します。

一連のプロパティのコンテキストは、 [**WIA\_プロパティ\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/ns-wiamindr_lh-_wia_property_context)構造に保持されます。これには、プロパティコンテキストのプロパティの数、プロパティ識別子の配列へのポインター (propids)、およびへのポインターという3つのメンバーが含まれます。ブール値の配列。 配列は並行して保持されます (つまり、プロパティ識別子の配列のプロパティ識別子がインデックス*N*のプロパティは、bool 配列内の同じインデックスにある bool 値に関連付けられています)。

ミニドライバーは、WIA サービスライブラリ関数[**Wiascreatepropcontext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatepropcontext)を呼び出して、メモリを割り当て、プロパティコンテキストの値を入力します。 [**Wiasgetchangedvaluefloat**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchangedvaluefloat)などの他の WIA サービスライブラリ関数では、プロパティコンテキストを使用して、プロパティの値をいつ更新するかを決定します。

 

 




