---
Description: 概念モデル
title: 概念モデル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8340e69edaf2b0b20492ff470ca2db6608723204
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380849"
---
# <a name="the-conceptual-model"></a>概念モデル


WPD 概念モデルでは、オブジェクト、プロパティ、およびリソースの観点からのデバイスについて説明します。 次のトピックでは、これらの要素について説明します。

## <a name="span-idobjectsspanspan-idobjectsspanspan-idobjectsspanobjects"></a><span id="Objects"></span><span id="objects"></span><span id="OBJECTS"></span>オブジェクト


WPD では、デバイス上の論理エンティティをオブジェクトと呼びます。 常にではありませんが、通常、デバイス上のデータを表現します。 オブジェクトは、プロパティ、およびオブジェクト識別子によって参照されます。 オブジェクトの例では、画像と、カメラ、曲およびメディア プレーヤー、携帯電話では、連絡先情報を再生リスト上のフォルダーを含めるし、具合です。

オブジェクトでは、デバイスの機能または情報の部分を表すこともできます。 これらの例には、プレーヤーのコントロール (再生/レコード/一時停止)、カメラの設定、携帯電話のショート メッセージ サービス (SMS) 機能、およびなどが含まれます。 オブジェクトには、バイナリ データ、リソースとして格納されていることもできます。

## <a name="span-idpropertiesspanspan-idpropertiesspanspan-idpropertiesspanproperties"></a><span id="Properties"></span><span id="properties"></span><span id="PROPERTIES"></span>プロパティ


オブジェクトのプロパティについて説明するオブジェクトのメタデータを交換するためのメカニズムを提供します。 たとえば、イメージ オブジェクトには、そのファイル名、サイズ、形式、幅 (ピクセル単位) で記述するプロパティを含めることができます。

プロパティは、現在の値と属性があります。 WPD には、一連の API および DDI の定義を構成する標準的なプロパティを定義します。 ベンダーは、定義済みの WPD プロパティに限定されないし、自由に、独自に追加します。

## <a name="span-idpropertyattributesspanspan-idpropertyattributesspanspan-idpropertyattributesspanproperty-attributes"></a><span id="Property_Attributes"></span><span id="property_attributes"></span><span id="PROPERTY_ATTRIBUTES"></span>プロパティの属性


プロパティの属性は、アクセス権を有効な値、およびプロパティに関連するその他の情報について説明します。 たとえば、プロパティを表すビットレートでしたする範囲 8 キロ ビット/秒 (Kbps) から 20 Kbps 1 Kbps のステップ値を持つです。

アクセス権を示すかどうかの呼び出し元の読み取り、書き込みしたりプロパティを削除します。 有効な値は、プロパティ値の制限を示します。 有効な値は、特定の形式であると見なされます。 有効な値のフォームには、範囲 (つまり、プロパティ値をとる最小値から指定されたステップの最大値に)、列挙型 (つまり、プロパティ値が指定されたリストのうちの 1 つ)、および None (つまり、ない特定の有効な値)。

## <a name="span-idresourcesspanspan-idresourcesspanspan-idresourcesspanresources"></a><span id="Resources"></span><span id="resources"></span><span id="RESOURCES"></span>リソース


リソースは、バイナリ データのプレース ホルダーです。 オブジェクトは、1 つ以上のリソースを持つことができます。 たとえば、オブジェクトにオーディオの注釈付きのイメージ ファイルが表されている場合、このオブジェクトのリソース可能性がありますようになります。

-   既定のリソース。 このリソースは、イメージ ファイル全体を表します。 (オーディオ注釈やサムネイルなどの任意の埋め込みデータを含む)
-   サムネイルのリソースです。 このリソースは、イメージのサムネイルのデータを表します。
-   オーディオ注釈リソースの場合です。 このリソースは、オーディオ、画像に関連付けられたデータを表します。

## <a name="span-idresourceattributesspanspan-idresourceattributesspanspan-idresourceattributesspanresource-attributes"></a><span id="Resource_Attributes"></span><span id="resource_attributes"></span><span id="RESOURCE_ATTRIBUTES"></span>リソース属性


プロパティの属性と同様に、リソースの属性について説明するアクセス権、サイズ、形式、およびリソースに関連するその他の情報。 たとえば、イメージ オブジェクトにオーディオ注釈リソースの属性では、ビット レート、チャネルの数、およびオーディオのデータ形式を指定できます。

## <a name="span-idobjectillustrationspanspan-idobjectillustrationspanspan-idobjectillustrationspanobject-illustration"></a><span id="Object_Illustration"></span><span id="object_illustration"></span><span id="OBJECT_ILLUSTRATION"></span>オブジェクトの図


次の図は、オブジェクト、そのプロパティ、および例として、イメージ オブジェクトを使用して、そのリソース間の関係を示します。

![wpd オブジェクト](images/wpd_overview_figure2.png)

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[**WPD ドライバーの概要**](wpd-drivers-overview.md)

 

 





