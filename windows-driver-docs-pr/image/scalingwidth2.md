---
title: /幅の要素 (出力ドキュメント)
description: 必須の scaling Ingwidth 要素には、出力ドキュメントの幅の調整に使用できる値の範囲が含まれています。
ms.assetid: 8b15f4b9-8537-479e-8745-0c8b35883bf5
keywords:
- 幅を持つ要素のイメージ化デバイス
topic_type:
- apiref
api_name:
- wscn ScalingWidth
api_type:
- Schema
ms.date: 07/06/2020
ms.localizationpriority: medium
ms.openlocfilehash: 29de9789434b4e3ee415ecf37eacc5795d1602ef
ms.sourcegitcommit: 40d7d538756767d26bbda636589f614f85a6fab3
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "86020072"
---
# <a name="scalingwidth-element-output-document"></a>/幅の要素 (出力ドキュメント)

必須の scaling **Ingwidth**要素には、出力ドキュメントの幅の調整に使用できる値の範囲が含まれています。

## <a name="usage"></a>使用

```xml
<wscn:ScalingWidth>
  child elements
</wscn:ScalingWidth>
```

## <a name="attributes"></a>属性

属性はありません。

## <a name="child-elements"></a>子要素

| 要素 |
|--|
| [**MaxValue**](maxvalue.md) |
| [**MinValue**](minvalue.md) |

## <a name="parent-elements"></a>親要素

| 要素 |
|--|
| [**ScalingRangeSupported**](scalingrangesupported.md) |

## <a name="remarks"></a>注釈

Scaling **Ingwidth**要素には、出力ドキュメントの幅を調整するためにスキャンデバイスでサポートされる最小値と最大値を指定する[**MinValue**](minvalue.md)要素と[**MaxValue**](maxvalue.md)要素が含まれています。

**MinValue**と**maxvalue**は、1 ~ 1000 の整数にする必要があります。 **MinValue**の値は**MaxValue**以下でなければなりません。 値100はスキャンデバイスがスキャンされたイメージの幅を調整してはいけないことを意味します。 少なくとも、WSD Scan サービスでは100の値がサポートされている必要があります。

## <a name="see-also"></a>こちらもご覧ください

[**MaxValue**](maxvalue.md)

[**MinValue**](minvalue.md)

[**ScalingHeight**](scalingheight2.md)

[**ScalingRangeSupported**](scalingrangesupported.md)
