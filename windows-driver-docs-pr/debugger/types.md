---
title: 型
description: 型
ms.assetid: 234f4f36-ccd3-426a-a361-33727e9ece5a
keywords:
- 型のシンボル
- 種類
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: be94f7ecbd120deea2a3f0d361adc4ccb90d2a67
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366352"
---
# <a name="types"></a>型


## <span id="ddk_types_dbx"></span><span id="DDK_TYPES_DBX"></span>


モジュールのシンボル ファイルから型情報は、2 つの情報で識別されます。 型 ID と、型が所属するモジュールのベース アドレス。 型 ID を調べるには、次のメソッドを使用できます。

-   [**GetTypeId** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-gettypeid)型 ID を指定した型名を返します。

-   [**GetSymbolTypeId** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-getsymboltypeid)型 ID を指定した名前のシンボルの種類を返します。

-   [**GetOffsetTypeId** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-getoffsettypeid)指定した場所にある記号の型 ID を返します。

名前と型のサイズがによって返される[ **GetTypeName** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-gettypename)と[ **GetTypeSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-gettypesize)、それぞれします。

ターゲットの物理および仮想メモリで型指定されたデータの読み書きには、次の便利なメソッドを使用できます。

[**ReadTypedDataPhysical**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-readtypeddataphysical)

[**WriteTypedDataPhysical**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-writetypeddataphysical)

[**ReadTypedDataVirtual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-readtypeddatavirtual)

[**WriteTypedDataVirtual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-writetypeddatavirtual)

### <a name="span-idprintingtypeddataspanspan-idprintingtypeddataspanprinting-typed-data"></a><span id="printing_typed_data"></span><span id="PRINTING_TYPED_DATA"></span>型指定されたデータの印刷

型指定されたデータをフォーマットして、出力のコールバックに送信するには、次のように使用します[ *OutputTypedDataPhysical* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-outputtypeddataphysical)と[ *OutputTypedDataVirtual* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-outputtypeddatavirtual)の。ターゲットの物理および仮想メモリ内のデータそれぞれします。

説明されている種類のオプション[**デバッグ\_TYPEOPTS\_XXX** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-typeopts-xxx)エンジンが出力コールバックに送信する前に型指定されたデータをフォーマットする方法に影響します。

使用して種類のオプションを有効に[ **AddTypeOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-addtypeoptions)を使用してになっていると[ **RemoveTypeOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-removetypeoptions)します。

[**GetTypeOptions** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-gettypeoptions)現在型オプションを返します。 一度にすべての種類のオプションを設定するには、使用[ **SetTypeOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-settypeoptions)します。

### <a name="span-idinterpretingrawdatausingtypeinformationspanspan-idinterpretingrawdatausingtypeinformationspaninterpreting-raw-data-using-type-information"></a><span id="interpreting_raw_data_using_type_information"></span><span id="INTERPRETING_RAW_DATA_USING_TYPE_INFORMATION"></span>型情報を使用して生データを解釈します。

型指定されたデータの解釈をサポートする API デバッガー エンジンです。 これにより、構造体のメンバーの検索、逆参照、ポインター、配列要素の検索など、ターゲットのオブジェクトの階層について説明します。

型指定されたデータがのインスタンスによって説明されている、 [**デバッグ\_型指定された\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ns-wdbgexts-_debug_typed_data)構造体であり、特定の型にキャストするターゲット上のメモリの領域を表します。 [**デバッグ\_要求\_EXT\_型指定された\_データ\_ANSI**](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-request-ext-typed-data-ansi)**要求**操作の使用これらのインスタンスを操作します。 これらは、結果の式またはメモリを指定した型のキャストのリージョンに初期化できます。 すべてのサブ操作の一覧をデバッグ\_要求\_EXT\_型指定された\_データ\_ANSI**要求**操作のサポートを参照してください[ **EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ne-wdbgexts-_ext_tdop)します。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、出力のコールバックは、次を参照してください。[入力と出力](using-input-and-output.md)します。

 

 





