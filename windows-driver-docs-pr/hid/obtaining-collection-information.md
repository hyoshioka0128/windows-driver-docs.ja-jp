---
title: コレクション情報を取得する
description: コレクション情報を取得する
ms.assetid: 0568993b-ff50-48ac-a875-95ab643d6c28
keywords:
- コレクションを非表示に WDK を素早く収集
- HID コレクション WDK、情報の収集
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 871aa3a668e7554dbb7002a313d2963c67067b60
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346189"
---
# <a name="obtaining-collection-information"></a>コレクション情報を取得する





このセクションではユーザー モード アプリケーションとカーネル モード ドライバー操作に使用する情報の取得、 [HID コレクション](hid-collections.md)します。

アプリケーション、ドライバーは、HID コレクションに接続されているが後、は、次の情報を取得できます。

-   [コレクションの機能](collection-capability.md)します。

-   [配列の機能をボタン](button-capability-arrays.md)と[機能の配列の値](value-capability-arrays.md)ボタンと、コレクションによってサポートされる値の機能を記述します。

-   リンク コレクション配列の内部組織の説明、その[リンク コレクション](link-collections.md)します。

この情報が含まれています、 [HID usage](hid-usages.md)コレクションとコレクションでサポートされているすべてのコントロールの。 場合は、アプリケーションやドライバーでは、これらのコントロールを使用していない、すぐに、コレクションへの接続を閉じること必要があります。

この情報を入手すると、アプリケーション、ドライバーは、HID レポート内のコントロールのデータにアクセスするために必要な情報です。

 

 




