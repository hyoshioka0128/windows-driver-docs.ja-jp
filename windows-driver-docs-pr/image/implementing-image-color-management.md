---
title: イメージ カラーの管理の実装
description: イメージ カラーの管理の実装
ms.assetid: b3184a8b-4f32-4cb0-8f68-777d85110142
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e03dc2d5f7fa8332ef233118a5285c89047c83c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373524"
---
# <a name="implementing-image-color-management"></a>イメージ カラーの管理の実装





WIA は、Microsoft Windows で提供されるイメージの色の管理 (ICM) システムに依存します。 ICM は、Microsoft Windows SDK ドキュメントで説明します。

最適なアプリケーション互換性のため、すべてミニドライバーは、sRGB 色空間にデータを返す必要があります。 デバイスに別の色空間内のデータがネイティブによって生成される場合、ミニドライバーは、sRGB にその出力をマップする ICM 関数を使用する必要があります。 一部のアプリケーションは ICM の実装し、ネイティブの色空間でのデータを取得することがあります。 ミニドライバーは、セットアップ情報 (INF) ファイルで、ネイティブの色空間を指定して、有効な値 1 を指定することによってこの機能を許可することができます、 [ **WIA\_IPA\_アプリ\_色\_マッピング**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-app-color-mapping)プロパティ。

アプリケーションは、1 をプロパティを設定、ミニドライバーを sRGB へのマッピングを停止し、マッピングを処理するためにアプリケーションを許可します。 アプリケーションの現在の値を使用して、 [ **WIA\_IPA\_ICM\_プロファイル\_名前**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-icm-profile-name)プロパティとして、デバイスからデータをプロファイルします。 ユーザーのシステム ダイアログを使用して、プロパティを設定して、ミニドライバーで変更しないでください。

 

 




