---
title: DeviceInfo XML ドキュメント
description: DeviceInfo XML ドキュメント
ms.assetid: b6b859cf-de30-4df0-bec1-0cd7d8c55ea6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0932c22db6d3bed51694728fcb27fe76d81d1441
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387114"
---
# <a name="deviceinfo-xml-document"></a>DeviceInfo XML ドキュメント


デバイスとプリンターのユーザー インターフェイスには、デバイスのメタデータのパッケージの DeviceInfo XML ドキュメントに基づいているデバイスに関する詳細情報が表示されます。 この XML ドキュメントには、次などのデバイスのプロパティを指定するデータが含まれています。

-   デバイスの機能のカテゴリ。 この情報がで指定された、 [ **DeviceCategory** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff541101(v=vs.85))子要素である XML 要素の[ **DeviceCategoryList** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff541102(v=vs.85)) XMLDeviceInfo XML ドキュメント内の要素。

    最初の[ **DeviceCategory** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff541101(v=vs.85))内の XML 要素、 [ **DeviceCategoryList** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff541102(v=vs.85)) XML 要素と見なされます、 *プライマリ機能カテゴリ*のデバイス。 デバイスとプリンターのユーザー インターフェイスは、コンピューターに接続されているデバイスのギャラリー ビューを最初に表示します。 または、エンドユーザーがデバイスをカテゴリでフィルター処理された場合、その主な機能のカテゴリに基づいてデバイスが表示されます。

    多機能デバイスは、他の機能カテゴリは、個別で指定された[ **DeviceCategory** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff541101(v=vs.85)) XML 子要素、最初に続く**DeviceCategory**内の要素、 [ **DeviceCategoryList** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff541102(v=vs.85)) XML 要素。 ここでも、エンドユーザーがデバイス カテゴリに基づいてデバイスとプリンターのユーザー インターフェイス内のデバイスをフィルター処理と、デバイスが、プライマリと追加の機能カテゴリに基づいて表示されます。

-   デバイスのモデル名。 この情報がで指定された、 [ **ModelName** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff549311(v=vs.85)) DeviceInfo XML ドキュメント内の XML 要素。

-   デバイスの説明。 この情報がで指定された、 [ **DeviceDescription1** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff541105(v=vs.85))と[ **DeviceDescription2** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff541108(v=vs.85)) DeviceInfo XML 内の XML 要素ドキュメントです。

-   デバイスの製造元。 この情報がで指定された、 [**製造元**](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff548710(v=vs.85)) DeviceInfo XML ドキュメント内の XML 要素。

-   デバイスを表すアイコン。 この情報がで指定された、 [ **DeviceIconFile** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff541123(v=vs.85)) DeviceInfo XML ドキュメント内の XML 要素。

    デバイス アイコンの詳細については、次を参照してください。[デバイス アイコン ファイル](device-icon-file.md)します。

各デバイス メタデータ パッケージは、1 つだけの DeviceInfo XML ドキュメントを含める必要があります。 ドキュメントの名前は、DeviceInfo.xml である必要があります。

DeviceInfo XML ドキュメント内のデータはに基づいて書式設定、 [DeviceInfo XML スキーマ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff541135(v=vs.85))します。

 

 





