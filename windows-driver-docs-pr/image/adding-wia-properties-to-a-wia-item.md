---
title: WIA 項目に WIA プロパティの追加
description: WIA 項目に WIA プロパティの追加
ms.assetid: 0cf4748f-c50a-4781-8b8d-3fb73e5d7242
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4522940e4279d4de8bde5672803edb0f3f4e88c1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557496"
---
# <a name="adding-wia-properties-to-a-wia-item"></a>WIA 項目に WIA プロパティの追加





WIA の各項目には、WIA プロパティが含まれています。 アプリケーションでは、読み取り、WIA WIA ミニドライバーを構成する項目のプロパティを書き込みます。 WIA サービスの呼び出し、 [ **IWiaMiniDrv::drvInitItemProperties** ](https://msdn.microsoft.com/library/windows/hardware/ff544989) WIA ミニドライバー アイテムのプロパティを初期化するために、アプリケーションにアクセスするすべての項目に対して 1 回のメソッド。 アプリケーション値の項目の WIA プロパティを書き込む、または読み取りない場合、その項目に対してこのメソッドは呼び出されません。 コンテキスト アイテムを*pWiasContext*にパラメーターが指すは、WIA プロパティを持つ項目が初期化されることを示します。

**IWiaMiniDrv::drvInitItemProperties**メソッドは、次のタスクを実行する必要があります。

1.  受信したデータを使用して、 *pWiasContext*項目の種類を決定するパラメーター。 WIA ミニドライバーを取得できます、 [IWiaDrvItem COM インターフェイス](iwiadrvitem-com-interface.md)呼び出して[ **wiasGetDrvItem**](https://msdn.microsoft.com/library/windows/hardware/ff549243)します。 このインターフェイスは、取得した後、 [ **IWiaDrvItem::GetItemFlags** ](https://msdn.microsoft.com/library/windows/hardware/ff543883) WIA 項目の種類を判断するメソッドを呼び出すことができます。

2.  プロパティの名前と現在の項目に必要な設定の完全なプロパティを記述するプロパティ Id の配列を作成します。 これらの配列を作成した後、WIA ミニドライバーを呼び出す必要があります、 [ **wiasSetItemPropNames** ](https://msdn.microsoft.com/library/windows/hardware/ff549369)関数のサービスを提供します。 この関数では、WIA サービス作成の配列に基づいて、WIA プロパティ セットを構築するように指示します。 この関数は、前に常に呼び出す必要があります[ **wiasWriteMultiple** ](https://msdn.microsoft.com/library/windows/hardware/ff549475)と[ **wiasSetItemPropAttribs**](https://msdn.microsoft.com/library/windows/hardware/ff549358)します。

3.  新しく作成された WIA プロパティに書き込み、初期または既定では、設定の値を設定します。 WIA ミニドライバーを呼び出す必要があります、 **wiasWriteMultiple**サービスの初期値を設定します。 この関数は、前に常に呼び出す必要があります**wiasSetItemPropAttribs**します。

4.  有効な値を作成し、各プロパティのアクセス権をします。 WIA ミニドライバーを呼び出す必要があります、 **wiasSetItemPropAttribs**サービスのアクセス権と有効な値を設定します。

**注**  読み取り (および再読み取り) のアプリケーションは、依存で、これによって、アプリケーションをプロパティの値の変更をキャッチすることにより、任意のプロパティ。
スキャナーとカメラの必須プロパティのセットがあります。 これらのプロパティの一覧は[WIA プロパティについて](about-wia-properties.md)します。

一部のプロパティでは、他のプロパティに依存関係があります。 たとえば、 [**形式**](https://msdn.microsoft.com/library/windows/hardware/ff551553)プロパティが依存、 [ **tymed** ](https://msdn.microsoft.com/library/windows/hardware/ff551656)プロパティ。 これらのプロパティの間の依存関係は、「 [WIA プロパティ](https://msdn.microsoft.com/library/windows/hardware/ff552739)します。

 

 

 




