---
title: 型
description: 型
ms.assetid: 234f4f36-ccd3-426a-a361-33727e9ece5a
keywords:
- 型のシンボル
- 種類
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b83cfdad72ec12d5f6beec0819dac1ed40f0605
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537730"
---
# <a name="types"></a>型


## <span id="ddk_types_dbx"></span><span id="DDK_TYPES_DBX"></span>


モジュールのシンボル ファイルから型情報は、2 つの情報で識別されます。 型 ID と、型が所属するモジュールのベース アドレス。 型 ID を調べるには、次のメソッドを使用できます。

-   [**GetTypeId** ](https://msdn.microsoft.com/library/windows/hardware/ff549376)型 ID を指定した型名を返します。

-   [**GetSymbolTypeId** ](https://msdn.microsoft.com/library/windows/hardware/ff549173)型 ID を指定した名前のシンボルの種類を返します。

-   [**GetOffsetTypeId** ](https://msdn.microsoft.com/library/windows/hardware/ff548062)指定した場所にある記号の型 ID を返します。

名前と型のサイズがによって返される[ **GetTypeName** ](https://msdn.microsoft.com/library/windows/hardware/ff549408)と[ **GetTypeSize**](https://msdn.microsoft.com/library/windows/hardware/ff549457)、それぞれします。

ターゲットの物理および仮想メモリで型指定されたデータの読み書きには、次の便利なメソッドを使用できます。

[**ReadTypedDataPhysical**](https://msdn.microsoft.com/library/windows/hardware/ff554344)

[**WriteTypedDataPhysical**](https://msdn.microsoft.com/library/windows/hardware/ff561463)

[**ReadTypedDataVirtual**](https://msdn.microsoft.com/library/windows/hardware/ff554345)

[**WriteTypedDataVirtual**](https://msdn.microsoft.com/library/windows/hardware/ff561466)

### <a name="span-idprintingtypeddataspanspan-idprintingtypeddataspanprinting-typed-data"></a><span id="printing_typed_data"></span><span id="PRINTING_TYPED_DATA"></span>型指定されたデータの印刷

型指定されたデータをフォーマットして、出力のコールバックに送信するには、次のように使用します[ *OutputTypedDataPhysical* ](https://msdn.microsoft.com/library/windows/hardware/ff553269)と[ *OutputTypedDataVirtual* ](https://msdn.microsoft.com/library/windows/hardware/ff553274)の。ターゲットの物理および仮想メモリ内のデータそれぞれします。

説明されている種類のオプション[**デバッグ\_TYPEOPTS\_XXX** ](https://msdn.microsoft.com/library/windows/hardware/ff541712)エンジンが出力コールバックに送信する前に型指定されたデータをフォーマットする方法に影響します。

使用して種類のオプションを有効に[ **AddTypeOptions**](https://msdn.microsoft.com/library/windows/hardware/ff537949)を使用してになっていると[ **RemoveTypeOptions**](https://msdn.microsoft.com/library/windows/hardware/ff554551)します。

[**GetTypeOptions** ](https://msdn.microsoft.com/library/windows/hardware/ff549428)現在型オプションを返します。 一度にすべての種類のオプションを設定するには、使用[ **SetTypeOptions**](https://msdn.microsoft.com/library/windows/hardware/ff556874)します。

### <a name="span-idinterpretingrawdatausingtypeinformationspanspan-idinterpretingrawdatausingtypeinformationspaninterpreting-raw-data-using-type-information"></a><span id="interpreting_raw_data_using_type_information"></span><span id="INTERPRETING_RAW_DATA_USING_TYPE_INFORMATION"></span>型情報を使用して生データを解釈します。

型指定されたデータの解釈をサポートする API デバッガー エンジンです。 これにより、構造体のメンバーの検索、逆参照、ポインター、配列要素の検索など、ターゲットのオブジェクトの階層について説明します。

型指定されたデータがのインスタンスによって説明されている、 [**デバッグ\_型指定された\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff541706)構造体であり、特定の型にキャストするターゲット上のメモリの領域を表します。 [**デバッグ\_要求\_EXT\_型指定された\_データ\_ANSI**](https://msdn.microsoft.com/library/windows/hardware/ff541547)**要求**操作の使用これらのインスタンスを操作します。 これらは、結果の式またはメモリを指定した型のキャストのリージョンに初期化できます。 すべてのサブ操作の一覧をデバッグ\_要求\_EXT\_型指定された\_データ\_ANSI**要求**操作のサポートを参照してください[ **EXT\_TDOP**](https://msdn.microsoft.com/library/windows/hardware/ff544529)します。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、出力のコールバックは、[入力と出力](using-input-and-output.md)を参照してください。

 

 





