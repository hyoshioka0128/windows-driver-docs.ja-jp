---
title: デバイス アイコン ファイル
description: デバイス アイコン ファイル
ms.assetid: bd1272d5-f673-4138-887d-94653cf41829
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf745b5da276f786d08c1ed102f3835d755981f2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362058"
---
# <a name="device-icon-file"></a>デバイス アイコン ファイル


デバイス メタデータ パッケージは、1 つの写真のような画像、またはデバイスとプリンターのユーザー インターフェイスでデバイスを表すアイコンに含めることができます。 イメージは、アイコン ファイルに格納され、ファイル名を指定する必要があります、 [ **DeviceIconFile** ](https://msdn.microsoft.com/library/windows/hardware/ff541123)のパッケージの要素[DeviceInfo XML ドキュメント](deviceinfo-xml-document.md)します。

デバイス メタデータ パッケージにデバイスのアイコン ファイルが含まれていないかどうか、 [ **DeviceIconFile** ](https://msdn.microsoft.com/library/windows/hardware/ff541123)要素、デバイスとプリンターのユーザー インターフェイスには、デバイスの既定のアイコンが表示されます。 このアイコンがで指定されているデバイスのカテゴリの種類に基づいて、 [ **DeviceCategory** ](https://msdn.microsoft.com/library/windows/hardware/ff541101) DeviceInfo XML ドキュメントの要素。

**注**  デバイス メタデータ パッケージを含むデバイス アイコン ファイル、デバイスとプリンターのユーザー インターフェイスでデバイスの写真のようなイメージを表示するために使用を強くお勧めします。 作成する方法の詳細が同じであるアイコンは Windows のグラフィック要素の特性を表示を参照してください[アイコン](https://docs.microsoft.com/visualstudio/extensibility/ux-guidelines/images-and-icons-for-visual-studio?view=vs-2017)Microsoft SDK に含まれています。

 

 

 





