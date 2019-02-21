---
title: 静止画像デバイスに対して色の管理
description: 静止画像デバイスに対して色の管理
ms.assetid: dfc4afad-221a-436c-9124-981a74f70ee3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0212d7682407b7af814421ca28130485cbee3147
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530828"
---
# <a name="color-management-for-still-image-devices"></a>静止画像デバイスに対して色の管理





ベンダーは、各静止画像デバイスの 1 つまたは複数のカラー プロファイルを提供する必要があります。 カラー プロファイル ファイル名は、ベンダーから提供された INF ファイルに含める必要があります。 デバイスは、sRGB データを生成する場合は、標準の色のシステム提供のプロファイルを指定できます*sRGB 色空間 Profile.icm*します。 インストーラーでは、指定のファイル名をコピーのいずれかに、[のレジストリ エントリは、デバイスを静止画像](registry-entries-for-still-image-devices.md)します。

デバイスは、別の色空間を使用してイメージを生成する場合は、さまざまなカラー プロファイルを使用する必要があります。 デバイスは、別の色空間の sRGB データまたはデータを生成、かどうかは、一貫して 1 つの色領域を使用する場合、最適な結果を取得するは。

静止画デバイスは、そのデータを送信する色空間の認識させる必要があります。 たとえば、ユーザーが (データ ソースの変更を許可するシステム) 上のガンマ レベルをリセットします。 アプリケーションはこの変更を認識できません。

色の管理の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

 

 




