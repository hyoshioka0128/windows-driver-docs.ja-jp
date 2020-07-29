---
title: センサー定数のカスタム値の定義 (以前のバージョン)
description: センサー定数のカスタム値の定義 (以前のバージョン)
ms.assetid: 0ed635c2-117d-4a49-a565-31e5a0a9861d
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3eb02dbc9a49e92ff2e7f9abf2ba941e26dadc69
ms.sourcegitcommit: 9102e34c3322d8697dbb6f9a1d78879147a73373
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/28/2020
ms.locfileid: "87264461"
---
# <a name="defining-custom-values-for-sensor-constants-previous-version"></a>センサー定数のカスタム値の定義 (以前のバージョン)


カテゴリ、センサーの種類、データフィールド、プロパティ、およびイベントのカスタム値を定義できます。

## <a name="guidelines-for-custom-values"></a>カスタム値のガイドライン

プラットフォーム定義定数のセットが機能する場合は、新しい定数を定義しないようにします。 「[定数](https://docs.microsoft.com/windows-hardware/drivers/sensors/about-sensor-constants)リファレンス」セクションで説明されているカテゴリ、型、データフィールド、プロパティ、およびイベントを調べ、理解し、センサードライバーがプラットフォームフレームワークに適合するかどうかを判断します。

カスタム値を定義する場合は、次のガイドラインに従ってください。

-   新しい PROPERTYKEYs を生成します。 プラットフォーム定義の定数から Guid を再利用しないでください。また、プラットフォームで定義されたベース値に新しい Guid を使用することはできません。

-   同じセンサーカテゴリの新しいセンサーデータ型に同一の Guid を使用します。 各データ型を一意にするには、プロパティキーの PID 部分をインクリメントします。

-   センサー用に定義した新しいセンサープロパティに同じ Guid を使用します。 各プロパティが一意になるようにするには、プロパティキーの PID 部分をインクリメントします。

-   センサー用に定義した新しいセンサーイベントの種類に同じ Guid を使用します。 各イベントの種類を一意にするには、プロパティキーの PID 部分をインクリメントします。

-   一意の定数を作成します。 定数名間の競合を回避するには、センサーコード内と他の実装間で名前を一意にするために役立つ値を使用して、各カスタム名を開始します。 たとえば、Fabrikam という会社では、を使用して各定数定義を開始でき `FABRIKAM_` ます。

-   値をドキュメント化して発行します。 開発者が Windows センサー API または Location API を使用してセンサーからのデータにアクセスできるようにするには、カスタム値を文書化し、定数を発行する必要があります。たとえば、ヘッダーファイルを指定します。 センサーが独自のシステムの一部である場合、カスタム値を発行する必要はありません。

## <a name="example"></a>例

センサー定数のカスタム値を定義する方法を次のコード例に示します。 この例では、現在の現地時刻を提供するサンプルセンサーの新しいカテゴリ、センサーの種類、およびデータ型を作成します。 このようなセンサーは、衛星またはその他の無線転送を使用して、参照クロックから時刻情報を受け取ることができます。

```cpp
// Define a sensor ID.
// {0D77BEE3-7169-42bf-8379-28F9A9B59A57}
DEFINE_GUID(SAMPLE_SENSOR_TIME_ID,
0xd77bee3, 0x7169, 0x42bf, 0x83, 0x79, 0x28, 0xf9, 0xa9, 0xb5, 0x9a, 0x57);

// Define a custom category.
// {062A5C3B-44C1-4ad1-8EFC-0F65B2E4AD48}
DEFINE_GUID(SAMPLE_SENSOR_CATEGORY_DATE_TIME,
0x62a5c3b, 0x44c1, 0x4ad1, 0x8e, 0xfc, 0xf, 0x65, 0xb2, 0xe4, 0xad, 0x48);

// Define a custom type.
// {5F199A84-409F-4e35-B2DD-F9C79F5318A0}
DEFINE_GUID(SAMPLE_SENSOR_TYPE_TIME,
0x5f199a84, 0x409f, 0x4e35, 0xb2, 0xdd, 0xf9, 0xc7, 0x9f, 0x53, 0x18, 0xa0);

// Time/Date sensor fields.
// Because these are related, each field uses the same GUID, but changes the PID.
// {340946F2-9A77-42b0-8176-57D4DF00E5CA}
DEFINE_PROPERTYKEY(SAMPLE_SENSOR_DATA_TYPE_HOUR,
0x340946f2, 0x9a77, 0x42b0, 0x81, 0x76, 0x57, 0xd4, 0xdf, 0x0, 0xe5, 0xca, PID_FIRST_USABLE); // PID = 2

DEFINE_PROPERTYKEY(SAMPLE_SENSOR_DATA_TYPE_MINUTE,
0x340946f2, 0x9a77, 0x42b0, 0x81, 0x76, 0x57, 0xd4, 0xdf, 0x0, 0xe5, 0xca, PID_FIRST_USABLE + 1); // PID = 3

DEFINE_PROPERTYKEY(SAMPLE_SENSOR_DATA_TYPE_SECOND,
0x340946f2, 0x9a77, 0x42b0, 0x81, 0x76, 0x57, 0xd4, 0xdf, 0x0, 0xe5, 0xca, PID_FIRST_USABLE + 2); // PID = 4
```

## <a name="using-the-define_propertykey-macro"></a>DEFINE \_ propertykey マクロの使用

DEFINE propertykey マクロを使用するには \_ 、次の2つのオプションのいずれかを使用します。

-   プロジェクトに Initguid を含めます。 この場合、マクロはプロパティキーを定義します。 この方法はほとんどの場合に機能しますが、大規模で複雑なプロジェクトでは名前の競合が発生する可能性があります。

-   Initguid を含めないでください。 代わりに、ファイル名拡張子が .lib のスタティックライブラリファイルに定義をコンパイルします。 この場合、マクロは、コンパイラのプロパティキーの名前を宣言します。 ただし、リンカー設定で .lib ファイルを参照する必要があります。 この方法は、複数のモジュールを使用する大規模なプロジェクトで最適に機能します。

Initguid を含めずにマクロを使用すると、ライブラリファイルを参照しないと、LNK2001 エラーが発生します。

## <a name="related-topics"></a>関連トピック
[センサーの地理位置情報ドライバーのサンプル](https://docs.microsoft.com/windows-hardware/drivers/gnss/sensors-geolocation-driver-sample)



