---
title: カスタム プロパティの使用
description: カスタム プロパティの使用
ms.assetid: cf4e728f-7900-4849-ab1c-135f9fec9713
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bec7fc3e78b0981fbb0e903c102e897ed247de05
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569783"
---
# <a name="using-custom-properties"></a>カスタム プロパティの使用





WIA ドライバーには、独自のカスタム プロパティを定義できます。 呼び出し元は、通常の WIA プロパティと同様、カスタム プロパティを操作できます。 ただし、アプリケーションまたはカスタム UI モジュールだけでは、これらのカスタム プロパティをアクセスできます。

WIA ドライバーは、WIA のオフセット プロパティ識別子へのカスタム プロパティを定義する必要があります\_プライベート\_デバイス プロパティ、および使用 WIA DEVPROP\_プライベート\_ITEMPROP の通常のアイテムのプロパティこのような内[ **IWiaMiniDrv::drvInitItemProperties**](https://msdn.microsoft.com/library/windows/hardware/ff544989)します。 詳細については、[カスタム プロパティを定義する](defining-custom-properties.md)を参照してください。

WIA ドライバーにカスタム パラメーターを渡す 2 つの方法はあります。

最初のオプションは、使用する、 **IWiaItemExtras::Escape**メソッド (Microsoft Windows SDK のドキュメントで説明)。 似ています、 [ **IStiUSD::Escape** ](https://msdn.microsoft.com/library/windows/hardware/ff543815)メソッドは、STI メソッドを使用する代わりに、直接、WIA を使用する呼び出し元を許可します。 使用して**IWiaItemExtras::Escape**、ドライバーのすべての情報を渡すことができ、ドライバーは、情報を渡すことができます。 WIA サービスは、呼び出し元とドライバーの間で渡されるバッファーのみを管理します。

2 番目のオプションでは、カスタム プロパティを使用します。 使用して、 **IWiaItemExtras::Escape**メソッドは、カスタムの WIA プロパティを使用するよりも柔軟性が WIA のカスタム プロパティでは、ドライバーが別の情報を読み取れるように、項目のプロパティのストリームの情報を格納できます。時間です。

次の 2 つのサンプル コード スニペットでは、カスタム プロパティを使用して、ドライバーからカスタム パラメーターを渡す方法を示します。

[カスタム プロパティを作成するサンプル コード](sample-code-to-create-custom-properties.md)

[カスタム プロパティを設定するサンプル コード](sample-code-to-set-custom-properties.md)

 

 




