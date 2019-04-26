---
title: WIA のプロパティ
description: WIA のプロパティ
ms.assetid: 3b9d4d90-775b-450e-b5d1-646ea45253d7
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23c0e4fc99f5b22bf16fe811c0dda7f554115c75
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352666"
---
# <a name="wia-properties"></a>WIA のプロパティ


## <span id="ddk_wia_properties_si"></span><span id="DDK_WIA_PROPERTIES_SI"></span>


このセクションには、WIA プロパティとその属性のすべてが含まれます。

これらのプロパティに関する参照トピックは、次の属性を一覧表示: プロパティの型、有効な値、およびアクセス権。

### <a name="span-idpropertytypesspanspan-idpropertytypesspanproperty-types"></a><span id="property_types"></span><span id="PROPERTY_TYPES"></span>プロパティの型

次の種類は、WIA でプロパティのデータ型を示すために使用されます。

<span id="VT_BSTR"></span><span id="vt_bstr"></span>VT\_BSTR  
Unicode 文字 (ワイド文字の文字列) の文字列。

<span id="VT_I4"></span><span id="vt_i4"></span>VT\_I4  
4 バイト整数。

<span id="VT_R4"></span><span id="vt_r4"></span>VT\_R4  
4 バイトの実数 (C **float**)。

<span id="VT_UI2"></span><span id="vt_ui2"></span>VT\_UI2  
2 バイト符号なし整数。

<span id="VT_VECTOR"></span><span id="vt_vector"></span>VT\_ベクター  
特定の型の要素の配列。 VT ともう 1 つのプロパティの型を組み合わせて場合\_OR 演算子の結果の値を使用するベクトルとは、DWORD 数は、最初に、ポインターに続く要素で構成される counted 配列の配列内の要素。 たとえば、VT\_UI2 |VT\_ベクトルが 2 バイト符号なし整数の要素の配列へのポインターの後に、DWORD の要素数。

### <a name="span-idvalidvaluesspanspan-idvalidvaluesspanvalid-values"></a><span id="valid_values"></span><span id="VALID_VALUES"></span>有効な値

次の種類は、1 つの値の範囲の値、値のリストまたはフラグとしてプロパティが存在するかどうかを示します。

<span id="WIA_PROP_NONE"></span><span id="wia_prop_none"></span>WIA\_PROP\_NONE  
プロパティには、1 つの値が含まれています。

<span id="WIA_PROP_RANGE"></span><span id="wia_prop_range"></span>WIA\_PROP\_範囲  
プロパティには、最小値、最大値、基準値、および増分を含む値の範囲が含まれています。

<span id="WIA_PROP_LIST"></span><span id="wia_prop_list"></span>WIA\_PROP\_一覧  
プロパティには、値の一覧が含まれています。

<span id="WIA_PROP_FLAG"></span><span id="wia_prop_flag"></span>WIA\_PROP\_フラグ  
プロパティには、フラグが含まれています。

### <a name="span-idaccessrightsspanspan-idaccessrightsspanaccess-rights"></a><span id="access_rights"></span><span id="ACCESS_RIGHTS"></span>アクセス権

プロパティの可能なアクセス権は次のとおりです。

<span id="Read-only"></span><span id="read-only"></span><span id="READ-ONLY"></span>読み取り専用  
ドライバーは、読み取り専用のアクセス権を持ちます。

<span id="Read_write"></span><span id="read_write"></span><span id="READ_WRITE"></span>読み取り/書き込み  
ドライバーはどちらも読み取りおよび書き込みアクセス。

上記のリストには、ここでは、WIA プロパティで使用されている型のみがについて説明します。 これらおよびその他のプロパティの型の詳細については、次を参照してください。 [ **WIA\_プロパティ\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff552751)します。

Windows SDK にはに関する情報が含まれて、 [WIA\_RAW\_ヘッダー](https://go.microsoft.com/fwlink/p/?linkid=153316)構造体。 WIA に関する情報も含まれています。\_イベント\_XXX と WIA\_CMD\_XXX 定数、で説明した、 [WIA イベント識別子](https://go.microsoft.com/fwlink/p/?linkid=153318)トピック。

 

 





