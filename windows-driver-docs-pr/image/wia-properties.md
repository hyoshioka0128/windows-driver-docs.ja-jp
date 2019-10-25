---
title: WIA のプロパティ
description: WIA のプロパティ
ms.assetid: 3b9d4d90-775b-450e-b5d1-646ea45253d7
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a4c9a443c367cdb6fef38a28c4955fe77249c17
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840672"
---
# <a name="wia-properties"></a>WIA のプロパティ


## <span id="ddk_wia_properties_si"></span><span id="DDK_WIA_PROPERTIES_SI"></span>


このセクションには、すべての WIA プロパティとその属性が含まれています。

これらのプロパティの参照トピックには、プロパティの型、有効な値、およびアクセス権の属性が一覧表示されます。

### <a name="span-idproperty_typesspanspan-idproperty_typesspanproperty-types"></a><span id="property_types"></span><span id="PROPERTY_TYPES"></span>プロパティの型

次の型は、プロパティのデータ型を示すために、WIA で使用されます。

<span id="VT_BSTR"></span><span id="vt_bstr"></span>VT\_BSTR  
Unicode 文字の文字列 (ワイド文字列)。

<span id="VT_I4"></span><span id="vt_i4"></span>VT\_I4  
4バイトの整数。

<span id="VT_R4"></span><span id="vt_r4"></span>VT\_R4  
4バイトの実数 (C の**float 型**)。

<span id="VT_UI2"></span><span id="vt_ui2"></span>VT\_UI2  
2バイト符号なし整数。

<span id="VT_VECTOR"></span><span id="vt_vector"></span>VT\_VECTOR  
特定の型の要素の配列。 または演算子を使用して別のプロパティ型と VT\_VECTOR を組み合わせると、結果として得られる値は、要素の DWORD 数で構成され、その後に配列内の最初の要素へのポインターを含むカウントされた配列になります。 たとえば、VT\_UI2 |VT\_VECTOR には DWORD 要素数があり、その後に2バイト符号なし整数要素の配列へのポインターが続きます。

### <a name="span-idvalid_valuesspanspan-idvalid_valuesspanvalid-values"></a><span id="valid_values"></span><span id="VALID_VALUES"></span>有効な値

次の型は、プロパティが単一の値、値の範囲、値のリスト、またはフラグとして存在するかどうかを示します。

<span id="WIA_PROP_NONE"></span><span id="wia_prop_none"></span>WIA\_PROP\_なし  
プロパティには、1つの値が含まれます。

<span id="WIA_PROP_RANGE"></span><span id="wia_prop_range"></span>WIA\_PROP\_範囲  
プロパティには、最小値、最大値、名目値、およびインクリメントを含む値の範囲が含まれます。

<span id="WIA_PROP_LIST"></span><span id="wia_prop_list"></span>WIA\_PROP\_一覧  
プロパティは、値のリストを格納します。

<span id="WIA_PROP_FLAG"></span><span id="wia_prop_flag"></span>WIA\_PROP\_フラグ  
プロパティにはフラグが含まれています。

### <a name="span-idaccess_rightsspanspan-idaccess_rightsspanaccess-rights"></a><span id="access_rights"></span><span id="ACCESS_RIGHTS"></span>アクセス権

次の一覧では、プロパティに対して使用できるアクセス権について説明します。

<span id="Read-only"></span><span id="read-only"></span><span id="READ-ONLY"></span>読み取り専用  
ドライバーには読み取り専用アクセスがあります。

<span id="Read_write"></span><span id="read_write"></span><span id="READ_WRITE"></span>読み取り/書き込み  
ドライバーには、読み取りと書き込みの両方のアクセス権があります。

上記のリストは、このセクションに含まれる WIA プロパティで使用されている型のみを示しています。 これらおよびその他のプロパティの種類の詳細については、「 [**WIA\_プロパティ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/ns-wiamindr_lh-_wia_property_info)」を参照してください。

Windows SDK には、 [WIA\_未加工\_ヘッダー](https://go.microsoft.com/fwlink/p/?linkid=153316)構造に関する情報が含まれています。 また、wia[イベント識別子](https://go.microsoft.com/fwlink/p/?linkid=153318)に関するトピックで説明されているように、WIA\_イベント\_XXX および WIA\_CMD\_xxx 定数に関する情報も含まれています。

 

 





