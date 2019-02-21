---
title: 地理的位置情報センサーをオブジェクトとして定義します。
description: シミュレートされたその地理的位置情報センサーは、センサー地理位置情報ドライバー サンプルは、オブジェクトとして扱います。
ms.assetid: CDAA93A1-9B20-4602-9A8A-A2C7CF52B576
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b578074781b44439f818ab1644d56e1abfc296ba
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531214"
---
# <a name="defining-the-geolocation-sensor-as-an-object"></a>地理的位置情報センサーをオブジェクトとして定義します。

> [!IMPORTANT] 
> このドキュメントと Windows 8.1 の地理的位置情報ドライバー サンプルが非推奨とされました。

シミュレートされたその地理的位置情報センサーは、センサー地理位置情報ドライバー サンプルは、オブジェクトとして扱います。 このオブジェクトは、geolocation.h をという名前のヘッダー ファイルで宣言されます。 (ヘッダー ファイルとその他のドライバーのサンプル ファイルの説明を参照してください[ドライバー ファイルのサンプル一覧](the-sample-driver-file-list.md)セクションです)。

ヘッダー ファイルには、擬似センサーでサポートされるプロパティを定義するデータ構造が含まれています。 さらに、ヘッダー ファイルには、次のようなメソッドの定義が含まれています。

-   [地理的位置情報オブジェクトを初期化します。](initializing-the-geolocation-object.md)
-   地理的位置情報のプロパティを取得または設定

という名前のソース ファイル内の対応するメソッドの定義にある: geolocation.cpp します。

ハードウェアをサポートするには、このサンプルを拡張するには、同様のヘッダーと宣言し、デバイスの対応するオブジェクトを定義するソース ファイルを作成します。 このサンプルを拡張する方法の詳細については、次を参照してください。[実際のハードウェアのサポートの追加](adding-support-for-actual-hardware.md)します。

## <a name="related-topics"></a>関連トピック
[実際のハードウェアのサポートの追加](adding-support-for-actual-hardware.md)  
[地理的位置情報オブジェクトを初期化します。](initializing-the-geolocation-object.md)  
[ドライバー ファイルのサンプル一覧](the-sample-driver-file-list.md)  



