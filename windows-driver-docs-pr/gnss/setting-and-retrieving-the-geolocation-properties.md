---
title: 設定と地理的位置情報のプロパティの取得
description: アプリケーションでは、特定のプロパティ値を取得するサンプル ドライバーに対応するプロパティの取得メソッドが呼び出されます。
ms.assetid: 576C610E-180A-44A0-9637-5C18341F3777
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2154b2fdabdd09c3f450b5e4132181669201dfd5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530599"
---
# <a name="setting-and-retrieving-the-geolocation-properties"></a>設定と地理的位置情報のプロパティの取得

> [!IMPORTANT] 
> このドキュメントと Windows 8.1 の地理的位置情報ドライバー サンプルが非推奨とされました。

アプリケーションでは、特定のプロパティ値を取得するサンプル ドライバーに対応するプロパティの取得メソッドが呼び出されます。 シミュレートされたセンサー、について**CGeolocation::GetPropertyValuesForGeolocationObject**します。 センサー API は、アプリケーションによって要求されたプロパティのプロパティのキーを渡すし、ドライバー内のプロパティ値のバンドル、 **IPortableDeviceValues** API に返されるオブジェクト。

アプリケーションの場合に書き込み、または (感度の変更や必要な正確性) プロパティを更新します。 サンプル ドライバーに対応するプロパティの書き込みメソッドが呼び出されます。 シミュレートされたセンサー、について**CGeolocation::UpdateGeolocationPropertyValues**します。 このメソッドが宣言され、センサー オブジェクトで定義されているファイル (Geolocation.h と Geolocation.cpp) のし、は、SensorDDI.cpp モジュールで呼び出されます。

センサーのプロパティを定義する方法については、[地理的位置情報のプロパティをサポートしている](supporting-the-geolocation-properties.md)を参照してください。

## <a name="related-topics"></a>関連トピック
[地理的位置情報オブジェクトを定義します。](defining-the-geolocation-object.md)  
[地理的位置情報のプロパティをサポートしています。](supporting-the-geolocation-properties.md)  



