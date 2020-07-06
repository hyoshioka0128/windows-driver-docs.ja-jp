---
title: 位置情報ドライバーのサンプルに実際のハードウェアのサポートを追加する
description: 位置情報ドライバーのサンプルは、GPS デバイスをシミュレートする出発点として提供されています。 このトピックでは、実際のハードウェアのサポートを追加する方法について説明します。
ms.assetid: 0D16C46F-4622-4191-83F2-579FC17DE985
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f541ff466138e36ce8e9898d016ca399234e230
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968355"
---
# <a name="adding-support-for-real-hardware-to-the-geolocation-driver-sample"></a>位置情報ドライバーのサンプルに実際のハードウェアのサポートを追加する

> [!IMPORTANT] 
> Windows 8.1 のこのドキュメントと位置情報ドライバーのサンプルは、非推奨とされました。

位置情報ドライバーのサンプルは、GPS デバイスをシミュレートする出発点として提供されています。 このトピックでは、実際のハードウェアのサポートを追加する方法について説明します。

位置情報のサンプルを使用して実際のハードウェアをサポートするために必要なリビジョンと追加については、次の表で簡単に説明します。 また、この表では、詳細情報が記載されている場所も示しています。

**リビジョンまたは追加**: 詳細情報

**新しいセンサーの目的を反映するようにソースファイルとヘッダーファイルの名前を変更します。詳細に**ついては、Windows Driver Kit のサンプルソースに含まれている readme (SensorsGeolocationSample.htm) の「サンプルのカスタマイズ」および「サンプルへのセンサーの追加」セクションを参照してください。

**位置情報プロパティを新しいセンサーでサポートされているプロパティに置き換えます。** Windows Driver Kit のサンプルソースに含まれている readme (SensorsGeolocationSample.htm) の「サンプルにセンサーを追加する」セクションを参照してください。

**新しいセンサーで必要なトランスポートをサポートするために必要なコードを含むモジュールを追加します。**


 

GPS (またはその他の位置情報) センサーを開発していて、HID トランスポートで実行されている場合は、デバイスを受信トレイ HID クラスドライバーと統合できます。

Windows Driver Kit に同梱されている readme ファイル SensorsGeolocationDriverSample.htm には、温度センサーをサポートするためにこのドライバーを変更する手順が含まれています。

**メモ**   センサーが HID 以外のトランスポートをサポートしている場合は、位置情報のサンプルに基づいて作成し、新しいドライバーの開始点として使用できます。 ただし、センサーで HID トランスポートがサポートされている場合は、受信トレイ HID クラスドライバーと互換性のあるファームウェアを作成する必要があります。

 

## <a name="related-topics"></a>関連トピック
[センサーの地理位置情報ドライバーのサンプル](sensors-geolocation-driver-sample.md)  



