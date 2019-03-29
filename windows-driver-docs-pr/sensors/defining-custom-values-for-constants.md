---
title: センサーの定数のカスタム値を定義します。
description: センサーの定数のカスタム値を定義します。
ms.assetid: 0ed635c2-117d-4a49-a565-31e5a0a9861d
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4474861e525c39e8b08bc952ed98eb773660782c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569934"
---
# <a name="defining-custom-values-for-sensor-constants"></a>センサーの定数のカスタム値を定義します。


カテゴリ、種類のセンサー、データ フィールド、プロパティ、およびイベントのカスタム値を定義することができます。

## <a name="guidelines-for-custom-values"></a>カスタム値に関するガイドライン

一連のプラットフォームで定義されている定数は機能がある場合、新しい定数を定義しないでください。 調査およびカテゴリ、種類、データ フィールド、プロパティ、およびイベントの説明を理解、[定数](https://msdn.microsoft.com/library/windows/hardware/ff545409)セクションを参照し、センサー ドライバーがプラットフォーム、フレームワークに収まるかどうかを決定します。

カスタム値を定義する場合は、これらのガイドラインに従います。

-   新しい PROPERTYKEYs を生成します。 プラットフォーム定義定数から Guid を再利用しないし、プラットフォーム定義の基本値では、新しい Guid を基本されません。

-   同じ Guid を使用して、同じセンサーのカテゴリで新しいセンサー データの型。 各データ型を一意にするには、プロパティのキーの PID 部分をインクリメントします。

-   センサー用に定義した新しいセンサー プロパティと同じ Guid を使用します。 各プロパティを一意にするには、プロパティのキー部の PID をインクリメントします。

-   センサー用に定義した新しいセンサー イベントの種類には、同じ Guid を使用します。 各イベントの種類を一意にするには、プロパティのキー部の PID をインクリメントします。

-   一意の定数を作成します。 定数の名前の競合を避けるためには、名前が一意で、センサー コード内と他の実装全体の両方になるときに役立つ値を持つ各カスタム名を開始します。 Fabrikam という名前の会社の各定数の定義の開始など`FABRIKAM_`します。

-   文書化し、値を公開します。 開発者は、Windows センサー API または場所 API を通じて、センサーからデータにアクセスできる場合は、カスタム値を文書化し、たとえばヘッダー ファイルを指定して、定数を発行する必要があります。 センサーが専用のシステムの一部である場合は、カスタム値を公開する必要はありません。

## <a name="example"></a>例

次のコード例では、カスタム センサー定数値を定義する方法を示します。 例では、新しいカテゴリをセンサーの種類、および現在の現地時刻を提供するサンプル センサーのデータ型を作成します。 衛星または無線他を通じて参照クロックから時刻の情報を受信するセンサーを想像できます。

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

## <a name="using-the-definepropertykey-macro"></a>定義を使用して\_PROPERTYKEY マクロ

定義を使用する\_PROPERTYKEY マクロは、次の 2 つのオプションのいずれかを使用します。

-   Initguid.h は、プロジェクトで使用します。 この場合、マクロに定義するプロパティのキー。 このアプローチでは、ほとんどの場合で機能しますが、大規模で複雑なプロジェクトの名前付けの競合が発生することができます。

-   Initguid.h は含まれません。 代わりに、.lib ファイル名拡張子を持つ静的ライブラリ ファイルに、定義をコンパイルします。 この場合、マクロは、コンパイラが、プロパティのキーの名前を宣言します。 ただし、リンカー設定で .lib ファイルを参照することがあります。 このアプローチは、複数のモジュールを使用して大規模なプロジェクトでは最適です。

Initguid.h を含むとライブラリ ファイルを参照することがなく、マクロの使用を LNK2001 エラーとなります。

## <a name="related-topics"></a>関連トピック
[センサー地理位置情報ドライバー サンプル](https://msdn.microsoft.com/library/windows/hardware/hh768273)



