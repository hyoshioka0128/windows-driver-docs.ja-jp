---
title: カスタム プロパティの使用
description: カスタム プロパティの使用
ms.assetid: cf4e728f-7900-4849-ab1c-135f9fec9713
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 435466f4a96f0c6b3d9178651ee98bb083114088
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385939"
---
# <a name="using-custom-properties"></a>カスタム プロパティの使用





WIA ドライバーには、独自のカスタム プロパティを定義できます。 呼び出し元は、通常の WIA プロパティと同様、カスタム プロパティを操作できます。 ただし、アプリケーションまたはカスタム UI モジュールだけでは、これらのカスタム プロパティをアクセスできます。

WIA ドライバーは、WIA のオフセット プロパティ識別子へのカスタム プロパティを定義する必要があります\_プライベート\_デバイス プロパティ、および使用 WIA DEVPROP\_プライベート\_ITEMPROP の通常のアイテムのプロパティこのような内[ **IWiaMiniDrv::drvInitItemProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinititemproperties)します。 詳細については、次を参照してください。[カスタム プロパティを定義する](defining-custom-properties.md)します。

WIA ドライバーにカスタム パラメーターを渡す 2 つの方法はあります。

最初のオプションは、使用する、 **IWiaItemExtras::Escape**メソッド (Microsoft Windows SDK のドキュメントで説明)。 似ています、 [ **IStiUSD::Escape** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-escape)メソッドは、STI メソッドを使用する代わりに、直接、WIA を使用する呼び出し元を許可します。 使用して**IWiaItemExtras::Escape**、ドライバーのすべての情報を渡すことができ、ドライバーは、情報を渡すことができます。 WIA サービスは、呼び出し元とドライバーの間で渡されるバッファーのみを管理します。

2 番目のオプションでは、カスタム プロパティを使用します。 使用して、 **IWiaItemExtras::Escape**メソッドは、カスタムの WIA プロパティを使用するよりも柔軟性が WIA のカスタム プロパティでは、ドライバーが別の情報を読み取れるように、項目のプロパティのストリームの情報を格納できます。時間です。

次の 2 つのサンプル コード スニペットでは、カスタム プロパティを使用して、ドライバーからカスタム パラメーターを渡す方法を示します。

[カスタム プロパティを作成するサンプル コード](sample-code-to-create-custom-properties.md)

[カスタム プロパティを設定するサンプル コード](sample-code-to-set-custom-properties.md)

 

 




