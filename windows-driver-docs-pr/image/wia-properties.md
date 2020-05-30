---
title: WIA のプロパティ
description: WIA のプロパティ
ms.assetid: 3b9d4d90-775b-450e-b5d1-646ea45253d7
ms.date: 05/29/2020
ms.localizationpriority: medium
ms.openlocfilehash: 192097f625abf4c76fcfd5ff0559449858e55199
ms.sourcegitcommit: 609c5731b2db4c17b9959082c4621c001e012db1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/30/2020
ms.locfileid: "84223571"
---
# <a name="wia-properties"></a>WIA のプロパティ

このセクションには、すべての WIA プロパティとその属性が含まれています。

これらのプロパティの参照トピックには、プロパティの型、有効な値、およびアクセス権の属性が一覧表示されます。

## <a name="property-types"></a>プロパティの型

次の型は、プロパティのデータ型を示すために、WIA で使用されます。

**VT \_ BSTR**

Unicode 文字の文字列 (ワイド文字列)。

**VT \_ I4**

4バイトの整数。

**VT \_ R4**

4バイトの実数 (C の**float 型**)。

**VT \_ UI2**

2 バイト符号なし整数。

**VT \_ ベクター**

特定の型の要素の配列。 または演算子を使用して別のプロパティの型を VT VECTOR と組み合わせると、 \_ 結果の値は、要素の DWORD 数で構成されるカウントされた配列になり、その後に配列内の最初の要素へのポインターが続きます。 たとえば、VT \_ UI2 |VT \_ VECTOR には DWORD 要素数が含まれ、その後に2バイト符号なし整数要素の配列へのポインターが続きます。

## <a name="valid-values"></a>有効な値

次の型は、プロパティが単一の値、値の範囲、値のリスト、またはフラグとして存在するかどうかを示します。

**WIA \_ PROP \_ NONE**

プロパティには、1つの値が含まれます。

**WIA \_ PROP の \_ 範囲**

プロパティには、最小値、最大値、名目値、およびインクリメントを含む値の範囲が含まれます。

**WIA の \_ PROP の \_ 一覧**

プロパティは、値のリストを格納します。

**WIA \_ PROP \_ フラグ**

プロパティにはフラグが含まれています。

## <a name="access-rights"></a>アクセス権

次の一覧では、プロパティに対して使用できるアクセス権について説明します。

**読み取り専用**

ドライバーには読み取り専用アクセスがあります。

**読み取り/書き込み** 

ドライバーには、読み取りと書き込みの両方のアクセス権があります。

## <a name="remarks"></a>解説

上記のリストは、このセクションに含まれる WIA プロパティで使用されている型のみを示しています。 

これらおよびその他のプロパティの種類の詳細については、「 [**WIA \_ プロパティの \_ 情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/ns-wiamindr_lh-_wia_property_info)」を参照してください。

Windows SDK には、WIA の[ \_ 未加工の \_ ヘッダー](https://docs.microsoft.com/windows/win32/wia/-wia-wia-raw-header)構造に関する情報が含まれています。

また、「Wia イベントの識別子」で説明されているように、WIA \_ イベント \_ XXX および wia CMD xxx の定数に関する情報も含まれてい \_ \_ ます。 [WIA Event Identifiers](https://docs.microsoft.com/windows/win32/wia/-wia-wia-event-identifiers)
