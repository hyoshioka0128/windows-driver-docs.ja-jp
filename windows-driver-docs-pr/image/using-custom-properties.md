---
title: カスタム プロパティの使用
description: カスタム プロパティの使用
ms.assetid: cf4e728f-7900-4849-ab1c-135f9fec9713
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3fc1a7f312ca3afd88c5272e492fd7d200e72789
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840728"
---
# <a name="using-custom-properties"></a>カスタム プロパティの使用





WIA ドライバーでは、独自のカスタムプロパティを定義できます。 呼び出し元は、通常の WIA プロパティと同じようにカスタムプロパティを操作できます。 ただし、これらのカスタムプロパティにアクセスできるのは、アプリケーションまたはカスタム UI モジュールだけです。

WIA ドライバーはカスタムプロパティを定義して、WIA によってオフセットされるプロパティ識別子をデバイスプロパティに対してプライベート\_DEVPROP\_します。また、内部[**などの通常の項目プロパティには、wia\_private\_ITEMPROP を使用します。IWiaMiniDrv::d rvInitItemProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinititemproperties)。 詳細については、「[カスタムプロパティの定義](defining-custom-properties.md)」を参照してください。

カスタムパラメーターを WIA ドライバーに渡すには、2つの方法があります。

最初のオプションでは、 **Iwiaitemextras:: Escape**メソッドを使用します (Microsoft Windows SDK のドキュメントを参照)。 これは、 [**Istiusd:: Escape**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-escape)メソッドに似ていますが、呼び出し元は、STI メソッドを使用する代わりに、WIA を直接使用することができます。 **Iwiaitemextras:: Escape**を使用すると、任意の情報をドライバーに渡すことができ、ドライバーは任意の情報を返すことができます。 WIA サービスは、呼び出し元とドライバーの間で渡されるバッファーのみを管理します。

2つ目のオプションは、カスタムプロパティを使用する方法です。 **Iwiaitemextras:: Escape**メソッドの使用はカスタム wia プロパティを使用するよりも柔軟ですが、カスタムの wia プロパティを使用すると、項目のプロパティストリームに情報を格納して、ドライバーが情報を別の時点で読み取ることができるようになります。

次の2つのサンプルコードスニペットは、カスタムプロパティを使用してドライバーとの間でカスタムパラメーターを渡す方法を示しています。

[カスタムプロパティを作成するためのサンプルコード](sample-code-to-create-custom-properties.md)

[カスタムプロパティを設定するサンプルコード](sample-code-to-set-custom-properties.md)

 

 




