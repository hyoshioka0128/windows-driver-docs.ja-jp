---
title: DeviceInfo XML ドキュメント
description: DeviceInfo XML ドキュメント
ms.assetid: b6b859cf-de30-4df0-bec1-0cd7d8c55ea6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b2441f9d33f9f594a618d3b4ad9858459255240
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356112"
---
# <a name="deviceinfo-xml-document"></a>DeviceInfo XML ドキュメント


デバイスとプリンターのユーザー インターフェイスには、デバイスのメタデータのパッケージの DeviceInfo XML ドキュメントに基づいているデバイスに関する詳細情報が表示されます。 この XML ドキュメントには、次などのデバイスのプロパティを指定するデータが含まれています。

-   デバイスの機能のカテゴリ。 この情報がで指定された、 [ **DeviceCategory** ](https://msdn.microsoft.com/library/windows/hardware/ff541101)子要素である XML 要素の[ **DeviceCategoryList** ](https://msdn.microsoft.com/library/windows/hardware/ff541102) XMLDeviceInfo XML ドキュメント内の要素。

    最初の[ **DeviceCategory** ](https://msdn.microsoft.com/library/windows/hardware/ff541101)内の XML 要素、 [ **DeviceCategoryList** ](https://msdn.microsoft.com/library/windows/hardware/ff541102) XML 要素と見なされます、 *プライマリ機能カテゴリ*のデバイス。 デバイスとプリンターのユーザー インターフェイスは、コンピューターに接続されているデバイスのギャラリー ビューを最初に表示します。 または、エンドユーザーがデバイスをカテゴリでフィルター処理された場合、その主な機能のカテゴリに基づいてデバイスが表示されます。

    多機能デバイスは、他の機能カテゴリは、個別で指定された[ **DeviceCategory** ](https://msdn.microsoft.com/library/windows/hardware/ff541101) XML 子要素、最初に続く**DeviceCategory**内の要素、 [ **DeviceCategoryList** ](https://msdn.microsoft.com/library/windows/hardware/ff541102) XML 要素。 ここでも、エンドユーザーがデバイス カテゴリに基づいてデバイスとプリンターのユーザー インターフェイス内のデバイスをフィルター処理と、デバイスが、プライマリと追加の機能カテゴリに基づいて表示されます。

-   デバイスのモデル名。 この情報がで指定された、 [ **ModelName** ](https://msdn.microsoft.com/library/windows/hardware/ff549311) DeviceInfo XML ドキュメント内の XML 要素。

-   デバイスの説明。 この情報がで指定された、 [ **DeviceDescription1** ](https://msdn.microsoft.com/library/windows/hardware/ff541105)と[ **DeviceDescription2** ](https://msdn.microsoft.com/library/windows/hardware/ff541108) DeviceInfo XML 内の XML 要素ドキュメントです。

-   デバイスの製造元。 この情報がで指定された、 [**製造元**](https://msdn.microsoft.com/library/windows/hardware/ff548710) DeviceInfo XML ドキュメント内の XML 要素。

-   デバイスを表すアイコン。 この情報がで指定された、 [ **DeviceIconFile** ](https://msdn.microsoft.com/library/windows/hardware/ff541123) DeviceInfo XML ドキュメント内の XML 要素。

    デバイス アイコンの詳細については、次を参照してください。[デバイス アイコン ファイル](device-icon-file.md)します。

各デバイス メタデータ パッケージは、1 つだけの DeviceInfo XML ドキュメントを含める必要があります。 ドキュメントの名前は、DeviceInfo.xml である必要があります。

DeviceInfo XML ドキュメント内のデータはに基づいて書式設定、 [DeviceInfo XML スキーマ](https://msdn.microsoft.com/library/windows/hardware/ff541135)します。

 

 





