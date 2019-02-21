---
title: センサーの定数について
description: センサーの定数について
ms.assetid: 9c26e305-0d5c-4442-9bcf-a9cdc1778c6b
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: fcc794e1f0e2d68bc074c5fa3ee349b1d831ce19
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538530"
---
# <a name="about-sensor-constants"></a>センサーの定数について


Windows Sensor and Location プラットフォームのさまざまな方法で使用される定数を使用します。 このセクションでは、これらの定数とその使用方法について説明します。

プラットフォームは、さまざまなセンサー ドライバーのコードで使用できる定数を定義します。 独自の定数を定義することもできます。 Sensors.h および Sensorsdef.h ファイル内のプラットフォームで定義されている定数の定義が表示されます。

## <a name="sensor-and-data-organization"></a>センサーとデータ編成

プラットフォームには、次の方法でのセンサーとそのデータが編成されています。

-   *カテゴリ*センサー デバイスの広範なクラスを表します。 カテゴリは、グループのセンサーのような種類の情報を提供する可能性が高いまたは何らかの方法で関連するそれ以外の場合をする方法を提供します。 各カテゴリは、GUID 定数で表されます。 レポートの緯度と経度の座標がによって表される位置センサー カテゴリに属するセンサーなど、 [**センサー\_カテゴリ\_場所**](sensor-category-loc.md)定数。

-   *種類のセンサー*センサーの特定の種類を表します。 各センサーの種類は、特定のカテゴリに適合します。 さまざまな種類の 2 つのセンサーは、同じカテゴリまたは 2 つの異なるカテゴリに属することができます。 各センサーの種類は、GUID 定数で表されます。 たとえば、グローバル配置 system センサー、センサーで識別されて\_型\_場所\_GPS 定数の場合、インターネットの IP アドレスを使用して現在の場所を提供するセンサーで識別されて中に、センサー\_型\_場所\_定数の参照。 ただし、両方のセンサーは場所のセンサーのカテゴリに属しています。

-   *データ型*センサーを提供する情報の特定の種類を表します。 センサーのデータ型は、高度、計器、およびデータでは、たとえば sea レベルの参照ポイントなど、データを express に使用されるユニットに関する情報など、実際の測定値の値を含めることができます。 によって表されるデータの種類ごと、 **PROPERTYKEY**定数。 たとえば、g's で x 軸の加速を表すデータ型は、センサーになります\_データ\_型\_アクセラレータ\_X\_G 定数。

-   格納される値といいますデータをレポートするときに、*データ フィールド*、関連するデータ フィールドのコレクションを構成して、*データ レポート*します。 使用してデータ レポートがまとめてパッケージ化、 [IPortableDeviceValues](https://go.microsoft.com/fwlink/p/?linkid=131486)インターフェイス。 各データ レポートには、少なくとも 1 つの有効なデータ フィールドとデータのレポートの作成時に識別するタイムスタンプを含める必要があります。 タイムスタンプが、センサーによって表される\_データ\_型\_タイムスタンプ プロパティのキー。


## <a name="other-constants"></a>その他の定数

ドライバーは、定数の他のいくつかの種類を使用する必要があります。 これらの定数は次のとおりです。

-   センサーなどのセンサー プロパティ\_プロパティ\_説明します。 これらの定数が WPD 定数、WPD などを含める\_機能\_オブジェクト\_カテゴリ。 場合など、センサーの記述にこれらの定数を使用する、通常でという[ **ISensorDriver::OnGetSupportedSensorObjects**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetsupportedsensorobjects)します。 によってプロパティ値を取得することも、 [ **ISensorDriver::OnGetSupportedProperties** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetsupportedproperties)と[ **ISensorDriver::OnGetProperties** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetproperties).

-   センサー プロパティは、ドライバーが提供する必要が、クライアント アプリケーションでいくつかのプロパティを設定することができます、常に同じ値を返すいくつか必要があります。 [**センサー プロパティ**](sensor-properties.md)リファレンス セクションの各プロパティのこの情報を提供します。 特定のメソッドに必要なプロパティを理解するには、メソッドのドキュメントを参照してください。、 [Windows センサー参照](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_sensors/#functions)セクション。

-   [**イベント定数**](about-sensor-driver-events.md)、センサーなど\_イベント\_状態\_変更しました。 イベント定数には、イベントの種類を表し、GUID、およびイベント パラメーターの型を表す、PROPERTYKEYs が含まれます。 これらの定数で、クラスの拡張機能によって呼び出されたときに使用する[ **ISensorDriver::OnGetSupportedEvents**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetsupportedevents)、を介してイベントを発生させる場合、または[ **ISensorClassExtension: PostEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-postevent)または[ **ISensorClassExtension::PostStateChange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-poststatechange)します。

-   アイコンの定数です。 ドライバーは、Windows のデバイスを表す特定のアイコンを指定できます。 参照してください[アイコンを指定する](specifying-an-icon.md)します。

-   センサー プラットフォームでは、センサー デバイス インターフェイスのクラスを識別するために、GUID_DEVINTERFACE_SENSOR 定数を定義します。 インストール中にドライバーは、インターフェイス クラスを少なくとも 1 つのデバイスを登録します。 センサー クラスの拡張機能では、センサー デバイス インターフェイスのクラスを登録します。



## <a name="persistent-unique-identifier"></a>永続的な一意識別子

センサーをという名前のセンサー プロパティ\_プロパティ\_持続\_UNIQUE\_ID には、特別な注意が必要です。 このプロパティの値は、デバイスで各センサーに対して一意である必要があります。 同時に、この値する必要がありますのままに一貫性のある特定のセンサーのセンサー プラットフォームでは、それを使用するたびにします。 ドライバーのコードで永続的な一意識別子を作成する方法の例は、次を参照してください。[永続的な一意の識別子を作成する](creating-a-persistent-unique-identifier.md)します。

## <a name="providing-geolocation-information"></a>地理的位置情報の情報を提供します。

場合があります、センサーの物理的な場所を把握するユーザーにとって重要な場合でも、センサーは、位置情報センサーではありません。 たとえば、気象観測ステーションを提供するデータの意味は、ステーションの場所に密接に関連付けられています。

この種類の地理的位置情報データを提供するすべてのセンサーがから適切なデータ フィールドを使用できます、 [**センサー\_カテゴリ\_場所**](sensor-category-loc.md)センサーが、場所にない場合でも、カテゴリセンサーです。 気象観測ステーション、センサーを使用してその場所のレポートをそのため、\_データ\_型\_緯度\_度とセンサー\_データ\_型\_経度\_度データ フィールドの定数。 ただし、これが重要で呼び出されると、場所、カテゴリに属するものとしては、このようなセンサーを報告しないようにする[ **ISensorDriver::OnGetProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetproperties)します。

Windows は、センサー、場所の種類のいずれかで、既存の場所のカテゴリとして扱います (センサー\_カテゴリ\_場所)。 その結果、これらのセンサーは、場所のアクセス許可モデルで分類されます。 位置情報センサーの権限モデルをバイパスしないで (たとえば、センサーとして、GPS センサーの種類を提示\_型\_場所\_GPS 場所以外のカテゴリを指定することが)。

## <a name="custom-values"></a>カスタム値

カテゴリ、種類のセンサー、データ フィールド、プロパティ、およびイベントのカスタム値を定義することができます。

ガイドラインと定数のカスタム値を定義する方法の例では、次を参照してください。[定数のカスタム値を定義する](defining-custom-values-for-constants.md)します。

 

 




