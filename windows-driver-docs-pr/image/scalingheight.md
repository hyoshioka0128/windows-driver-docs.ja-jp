---
title: /高さ要素 (低速スキャンの方向)
description: 必要な scaling Ingheight 要素は、低速スキャンの方向のドキュメントスケーリングを指定します。
ms.assetid: 29dcaab0-d32b-4aa0-ba27-3da0c9c39f97
keywords:
- スケールアウト要素のイメージ化デバイス
topic_type:
- apiref
api_name:
- wscn ScalingHeight wscn Override "" wscn UsedDefault ""
api_type:
- Schema
ms.date: 07/06/2020
ms.localizationpriority: medium
ms.openlocfilehash: fb23d3bd7cfe7ce49aff28955f52233172f74df0
ms.sourcegitcommit: 40d7d538756767d26bbda636589f614f85a6fab3
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "86020079"
---
# <a name="scalingheight-element-slow-scan-direction"></a>/高さ要素 (低速スキャンの方向)

必要な scaling **Ingheight**要素は、低速スキャンの方向のドキュメントスケーリングを指定します。

## <a name="usage"></a>使用

```xml
<wscn:ScalingHeight wscn:Override="" wscn:UsedDefault=""
  Override = "xs:string"
  UsedDefault = "xs:string">
  text
</wscn:ScalingHeight wscn:Override="" wscn:UsedDefault="">
```

## <a name="attributes"></a>属性

| 属性 | Type | 必須 | Description |
|--|--|--|--|
| **オーバーライド** | xs:string | いいえ | 省略可能。 0、false、1、または true である必要があるブール値。 |
| **既定値を使う** | xs:string | いいえ | 省略可能。 0、false、1、または true である必要があるブール値。 |

## <a name="text-value"></a>テキスト値

必須です。 1 ~ 1000 の範囲の整数。

## <a name="child-elements"></a>子要素

子要素はありません。

## <a name="parent-elements"></a>親要素

| 要素 |
|--|
| [**Scaling**](scaling.md) |

## <a name="remarks"></a>注釈

Scaling **Ingheight**要素は、低速スキャンの方向に適用するスケールファクターを指定します。 スケーリングは1パーセント単位で表されます。100の値は、100% の幅スケール (ドキュメントの高さに合わせて調整されません) を示します。

すべての WSD Scan サービスで、少なくとも100の値がサポートされている必要があります。

WSD スキャンサービスでは、値が**Documentfinalparameters**階層内に含まれ**ている**場合にのみ、オプションの**上書き**と使用される**既定**の属性を指定できます。 **オーバーライド**と使用される**既定値**とその使用方法の詳細については、「 [**documentfinalparameters**](documentfinalparameters.md)」を参照してください。

この要素に使用できる値は、サブセットにすることができます。

## <a name="see-also"></a>こちらもご覧ください

[**DocumentFinalParameters**](documentfinalparameters.md)

[**Scaling**](scaling.md)

[**ScalingWidth**](scalingwidth.md)
