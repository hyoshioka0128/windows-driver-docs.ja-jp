---
title: センサー クラスの拡張機能について
description: センサー クラスの拡張機能について
ms.assetid: 4b55e5fe-2947-4511-ba2d-479d5fd83ebe
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: e4b54940ff286a4c5bc794bd16f948a59ae128a6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363176"
---
# <a name="about-the-sensor-class-extension"></a>センサー クラスの拡張機能について


センサーを Windows (および特に sensor and location プラットフォーム)、Windows を公開しているデバイス ドライバーには、センサー ドライバー クラスの拡張が含まれていますを記述しやすく[ISensorClassExtension](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nn-sensorsclassextension-isensorclassextension)インターフェイス。 センサー デバイス ドライバーの必要なコンポーネントは、この COM オブジェクトでは、多数の定型コードを記述することがなくセンサー ドライバーを実装するためにプログラマが有効にするインターフェイスの単純なセットを提供します。 さらに、このクラスの拡張機能では、次の利点があります。

-   個人情報を処理するセンサーのコントロールの制約にアクセスしてクラスの拡張機能が適切な強制されるため、ユーザーのプライバシーがも保護されていることを確認するために役立ちます。

-   ドライバーからデータを取得し、API レイヤーを介してイベント通知を発生させる、標準的な方法を提供します。

 

 




