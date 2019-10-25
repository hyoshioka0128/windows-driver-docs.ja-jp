---
title: センサー クラスの拡張機能について
description: センサー クラスの拡張機能について
ms.assetid: 4b55e5fe-2947-4511-ba2d-479d5fd83ebe
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: a540856abf97e7eccf22a42e1b79951e7c15d70d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842372"
---
# <a name="about-the-sensor-class-extension"></a>センサー クラスの拡張機能について


センサーを Windows に公開するデバイスドライバー (特にセンサーと場所のプラットフォーム) を簡単に記述できるように、Windows にはセンサードライバーのクラス拡張[ISensorClassExtension](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nn-sensorsclassextension-isensorclassextension)インターフェイスが含まれています。 センサーデバイスドライバーに必要なコンポーネントです。この COM オブジェクトは、プログラマが多くの定型コードを記述せずにセンサードライバーを実装できるようにするためのシンプルなインターフェイスセットを提供します。 また、このクラス拡張には次のような利点があります。

-   クラス拡張によって、個人情報を処理するセンサーに対する適切なアクセス制御制限が適用されるため、ユーザーのプライバシーが確実に保護されます。

-   ドライバーからデータを取得し、API レイヤーを介してイベント通知を発生させるための標準的な方法を提供します。

 

 




