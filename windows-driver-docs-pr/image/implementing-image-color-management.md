---
title: イメージ カラーの管理の実装
description: イメージ カラーの管理の実装
ms.assetid: b3184a8b-4f32-4cb0-8f68-777d85110142
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85a3afdc65b1bd70b5f235935b572587cf1289b5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362078"
---
# <a name="implementing-image-color-management"></a>イメージ カラーの管理の実装





WIA は、Microsoft Windows で提供されるイメージの色の管理 (ICM) システムに依存します。 ICM は、Microsoft Windows SDK ドキュメントで説明します。

最適なアプリケーション互換性のため、すべてミニドライバーは、sRGB 色空間にデータを返す必要があります。 デバイスに別の色空間内のデータがネイティブによって生成される場合、ミニドライバーは、sRGB にその出力をマップする ICM 関数を使用する必要があります。 一部のアプリケーションは ICM の実装し、ネイティブの色空間でのデータを取得することがあります。 ミニドライバーは、セットアップ情報 (INF) ファイルで、ネイティブの色空間を指定して、有効な値 1 を指定することによってこの機能を許可することができます、 [ **WIA\_IPA\_アプリ\_色\_マッピング**](https://msdn.microsoft.com/library/windows/hardware/ff551521)プロパティ。

アプリケーションは、1 をプロパティを設定、ミニドライバーを sRGB へのマッピングを停止し、マッピングを処理するためにアプリケーションを許可します。 アプリケーションの現在の値を使用して、 [ **WIA\_IPA\_ICM\_プロファイル\_名前**](https://msdn.microsoft.com/library/windows/hardware/ff551571)プロパティとして、デバイスからデータをプロファイルします。 ユーザーのシステム ダイアログを使用して、プロパティを設定して、ミニドライバーで変更しないでください。

 

 




