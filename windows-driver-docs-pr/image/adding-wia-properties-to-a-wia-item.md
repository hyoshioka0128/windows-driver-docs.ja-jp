---
title: WIA 項目への WIA プロパティの追加
description: WIA 項目への WIA プロパティの追加
ms.assetid: 0cf4748f-c50a-4781-8b8d-3fb73e5d7242
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b4265ef8fbf1fa24ab94200802f773d9ea57b8d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840902"
---
# <a name="adding-wia-properties-to-a-wia-item"></a>WIA 項目への WIA プロパティの追加





各 WIA 項目には、WIA のプロパティが含まれています。 アプリケーションは、wia 項目のプロパティを読み取り、書き込み、WIA ミニドライバーを構成します。 WIA サービスは、アプリケーションがアクセスするすべての項目に対して[**IWiaMiniDrv::D rvinititemproperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinititemproperties)メソッドを1回呼び出し、その wia ミニドライバー項目のプロパティを初期化します。 アプリケーションで項目の WIA プロパティの読み取りまたは書き込みが行われない場合、その項目に対してこのメソッドは呼び出されません。 *Pwiascontext*パラメーターが指す項目コンテキストは、どの項目が WIA プロパティで初期化されるかを示します。

**IWiaMiniDrv::D rvinititemproperties**メソッドでは、次のタスクを実行する必要があります。

1.  *Pwiascontext*パラメーターで受け取ったデータを使用して、項目の種類を決定します。 WIA ミニドライバーは、 [**wiasGetDrvItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetdrvitem)を呼び出すことによって[IWiaDrvItem COM インターフェイス](iwiadrvitem-com-interface.md)を取得できます。 このインターフェイスを取得した後、 [**IWiaDrvItem:: GetItemFlags**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-getitemflags)メソッドを呼び出して、WIA 項目の種類を決定できます。

2.  現在の項目に必要な完全なプロパティセットを記述するプロパティ名とプロパティ Id の配列を作成します。 これらの配列を作成した後、WIA ミニドライバーは[**wiasSetItemPropNames**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassetitempropnames) service 関数を呼び出す必要があります。 この関数は、作成された配列に基づいて WIA プロパティセットを作成するように、WIA サービスに指示します。 この関数は、常に[**wiasWriteMultiple**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritemultiple)と[**wiasSetItemPropAttribs**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassetitempropattribs)の前に呼び出す必要があります。

3.  新しく作成された WIA プロパティセットに、初期値、つまり既定の設定値を書き込みます。 WIA ミニドライバーは、 **wiasWriteMultiple** service 関数を呼び出して初期値を設定する必要があります。 この関数は、常に**wiasSetItemPropAttribs**の前に呼び出す必要があります。

4.  各プロパティに有効な値とアクセス権を記述します。 WIA ミニドライバーは、 **wiasSetItemPropAttribs** service 関数を呼び出して、アクセス権と有効な値を設定する必要があります。

アプリケーションは、依存しているすべてのプロパティの読み取り (および読み取り) を行うので、アプリケーションはプロパティ値の変更をキャッチ**することができます  。**
スキャナーとカメラには、一連の必須プロパティがあります。 これらのプロパティについては、「 [ABOUT WIA properties](about-wia-properties.md)」をご覧ください。

一部のプロパティは、他のプロパティに依存しています。 たとえば、"[**書式**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-format)" プロパティは[**tymed**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-tymed)プロパティに依存します。 これらのプロパティ間の依存関係については、「 [WIA のプロパティ](https://docs.microsoft.com/windows-hardware/drivers/image/wia-properties)」を対象としています。

 

 

 




