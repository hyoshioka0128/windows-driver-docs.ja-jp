---
title: センサーの定数について
description: センサーの定数について
ms.assetid: 9c26e305-0d5c-4442-9bcf-a9cdc1778c6b
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7bc3f7cdd45c94f1b0fb8e7a0f991c6e42992568
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842380"
---
# <a name="about-sensor-constants"></a>センサー定数について


Windows センサーと場所のプラットフォームでは、さまざまな方法で定数を使用します。 ここでは、これらの定数とその使用法について説明します。

このプラットフォームでは、センサードライバーのコードで使用できるさまざまな定数を定義しています。 独自の定数を定義することもできます。 プラットフォームで定義された定数の定義は、ファイルの「センサー. h」と「Sensorsdef. h」で確認できます。

## <a name="sensor-and-data-organization"></a>センサーとデータの編成

このプラットフォームでは、次の方法でセンサーとそのデータを編成します。

-   *カテゴリ*は、さまざまなセンサーデバイスのクラスを表します。 カテゴリは、類似した種類の情報を提供する可能性があるセンサーをグループ化する方法を提供します。または、何らかの方法で関連します。 各カテゴリは GUID 定数で表されます。 たとえば、緯度と経度の座標を報告するセンサーは、[**センサー\_カテゴリ\_位置**](sensor-category-loc.md)定数で表される location センサーカテゴリに属します。

-   *センサーの種類*は、特定の種類のセンサーを表します。 各センサーの種類は、特定のカテゴリに収まります。 異なる種類の2つのセンサーは、同じカテゴリまたは2つの異なるカテゴリに属することができます。 各センサーの種類は、GUID 定数で表されます。 たとえば、グローバルポジショニングシステムセンサーはセンサー\_TYPE\_LOCATION\_GPS 定数によって識別されますが、インターネット IP アドレスを使用して現在の場所を提供するセンサーはセンサーによって識別され\_参照定数\_\_の場所を入力します。 ただし、両方のセンサーは location センサーカテゴリに属しています。

-   *データ型*は、センサーが提供できる特定の種類の情報を表します。 センサーのデータ型には、高度などの実際の測定値、データの表現に使用される単位に関する情報 (メーターなど)、データの参照ポイント (sea レベルなど) を含めることができます。 各データ型は**Propertykey**定数で表されます。 たとえば、g の x 軸加速度を表すデータ型は、センサー\_データ\_型\_高速化\_X\_G 定数です。

-   データをレポートする場合、値は*データフィールド*に含まれ、関連するデータフィールドのコレクションによって*データレポート*が構成されます。 データレポートは、 [Iportabledevicevalues](https://go.microsoft.com/fwlink/p/?linkid=131486)インターフェイスを使用してまとめてパッケージ化されます。 各データレポートには、少なくとも1つの有効なデータフィールドと、データレポートが作成された日時を示すタイムスタンプが含まれている必要があります。 タイムスタンプはセンサー\_データ\_型\_タイムスタンププロパティキーによって表されます。


## <a name="other-constants"></a>その他の定数

ドライバーでは、他の種類の定数も使用する必要があります。 これらの定数は次のとおりです。

-   センサー\_プロパティ\_の説明などのセンサーのプロパティ。 これらの定数には、WPD 定数 (たとえば、WPD\_機能\_オブジェクト\_カテゴリなど) が含まれています。 通常、これらの定数は、 [**ISensorDriver:: OnGetSupportedSensorObjects**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetsupportedsensorobjects)で呼び出された場合など、センサーを説明するために使用されます。 また、 [**ISensorDriver:: OnGetSupportedProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetsupportedproperties)と[**ISensorDriver:: OnGetProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetproperties)を使用してプロパティ値を返します。

-   一部のセンサープロパティはドライバーによって提供される必要があり、一部のプロパティはクライアントアプリケーションによって設定でき、一部のプロパティは常に同じ値を返す必要があります。 [**センサーのプロパティ**](sensor-properties.md)のリファレンスセクションには、各プロパティに関する情報が記載されています。 特定のメソッドに必要なプロパティを理解するには、「 [Windows センサーリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_sensors/#functions)」セクションのメソッドのドキュメントを参照してください。

-   センサー\_イベント\_状態\_変更された[**イベント定数**](about-sensor-driver-events.md)。 イベント定数には、イベントの種類を表す GUID、およびイベントパラメーターの型を表す PROPERTYKEYs が含まれます。 これらの定数は、 [**ISensorDriver:: OnGetSupportedEvents**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetsupportedevents)のクラス拡張によって呼び出されたとき、または[**ISensorClassExtension::P ostevent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-postevent)または[**ISensorClassExtension::P oststatechange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-poststatechange)を使用してイベントを発生させるときに使用します。

-   アイコン定数。 ドライバーは、Windows のデバイスを表す特定のアイコンを指定できます。 「[アイコンを指定する」を](specifying-an-icon.md)参照してください。

-   センサープラットフォームは、センサーデバイスインターフェイスクラスを識別するために GUID_DEVINTERFACE_SENSOR 定数を定義します。 インストール中に、ドライバーは少なくとも1つのデバイスインターフェイスクラスを登録します。 センサークラス拡張は、センサーデバイスインターフェイスクラスを登録します。



## <a name="persistent-unique-identifier"></a>永続的な一意識別子

センサー\_プロパティ\_永続的\_一意の\_ID というセンサープロパティには、特に注意が必要です。 このプロパティの値は、デバイスのセンサーごとに一意である必要があります。 同時に、センサープラットフォームがセンサーを使用するたびに、この値は特定のセンサーに対して一貫した状態に保つ必要があります。 ドライバーコードで永続的な一意識別子を作成する方法の例については、「[永続的な一意識別子の作成](creating-a-persistent-unique-identifier.md)」を参照してください。

## <a name="providing-geolocation-information"></a>位置情報情報の提供

センサーが位置センサーでない場合でも、ユーザーがセンサーの物理的な場所を知ることが重要になることがあります。 たとえば、気象局によって提供されるデータの意味は、ステーションの場所と密接に結び付いています。

この種類の地理位置情報データを提供するために、センサーが位置センサーでない場合でも、センサー [ **\_カテゴリ\_場所**](sensor-category-loc.md)カテゴリの適切なデータフィールドをセンサーで使用できます。 したがって、weather 局はセンサー\_データ\_TYPE\_緯度\_度およびセンサー\_データ\_の種類\_経度\_度データフィールド定数を使用して場所を報告できます。 ただし、 [**ISensorDriver:: OnGetProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetproperties)で呼び出された場合、Location カテゴリに属するセンサーを報告しないことが重要です。

Windows では、場所のカテゴリ (センサー\_カテゴリ\_の場所) の既存の場所の種類としてセンサーを扱います。 その結果、これらのセンサーは location アクセス許可モデルに含まれます。 位置センサーのアクセス許可モデルをバイパスすることは避けてください (たとえば、gps センサーの種類をセンサーとして表示したり、GPS\_GPS ではなく、場所以外のカテゴリを指定したりする\_場所に\_ます)。

## <a name="custom-values"></a>カスタム値

カテゴリ、センサーの種類、データフィールド、プロパティ、およびイベントのカスタム値を定義できます。

ガイドラインと、定数のカスタム値を定義する方法の例については、「[定数のカスタム値の定義](defining-custom-values-for-constants.md)」を参照してください。

 

 




