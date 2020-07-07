---
title: /高さ要素 (出力ドキュメントの高さ)
description: 必須の scaling Ingheight 要素には、出力ドキュメントの高さを調整するために使用できる値の範囲が含まれています。
ms.assetid: f13e1ef8-e05f-4aab-bf2a-08a953638334
keywords:
- スケールアウト要素のイメージ化デバイス
topic_type:
- apiref
api_name:
- wscn ScalingHeight
api_type:
- Schema
ms.date: 07/06/2020
ms.localizationpriority: medium
ms.openlocfilehash: 1ea1521fbb01257eb89d69d4d597dc1631f03137
ms.sourcegitcommit: 40d7d538756767d26bbda636589f614f85a6fab3
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "86020077"
---
# <a name="scalingheight-element-output-document-height"></a>/高さ要素 (出力ドキュメントの高さ)

必須の scaling **Ingheight**要素には、出力ドキュメントの高さを調整するために使用できる値の範囲が含まれています。

## <a name="usage"></a>使用

```xml
<wscn:ScalingHeight>
  child elements
</wscn:ScalingHeight>
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

Scaling **Ingheight**要素には、スキャンデバイスが出力ドキュメントの高さを調整するためにサポートする最小値と最大値を指定する[**MinValue**](minvalue.md)要素と[**MaxValue**](maxvalue.md)要素が含まれています。

**MinValue**と**maxvalue**は、1 ~ 1000 の整数にする必要があります。 **MinValue**の値は**MaxValue**以下でなければなりません。 値100はスキャンデバイスがスキャンされたイメージの高さに対して調整を行うことができないことを意味します。 少なくとも、WSD Scan サービスでは100の値がサポートされている必要があります。

## <a name="see-also"></a>こちらもご覧ください

[**MaxValue**](maxvalue.md)

[**MinValue**](minvalue.md)

[**ScalingRangeSupported**](scalingrangesupported.md)

[**ScalingWidth2**](scalingwidth.md)
