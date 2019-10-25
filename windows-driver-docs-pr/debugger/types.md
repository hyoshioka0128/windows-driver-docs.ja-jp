---
title: 型
description: 型
ms.assetid: 234f4f36-ccd3-426a-a361-33727e9ece5a
keywords:
- シンボル、型
- types
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 671b0f5145e2f53fe9b50828dc62737445bd220b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838805"
---
# <a name="types"></a>型


## <span id="ddk_types_dbx"></span><span id="DDK_TYPES_DBX"></span>


モジュールのシンボルファイルからの型情報は、型 ID と、その型が属するモジュールのベースアドレスの2つの情報によって識別されます。 型 ID を検索するには、次のメソッドを使用できます。

-   [**GetTypeId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-gettypeid)は、指定された型名の型 ID を返します。

-   [**Getsymbol typeid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getsymboltypeid)は、指定された名前を持つシンボルの型の ID を返します。

-   [**Getoffsettypeid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getoffsettypeid)は、指定された場所で見つかったシンボルの型 ID を返します。

型の名前とサイズは、それぞれ[**Gettypename**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-gettypename)と[**GetTypeSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-gettypesize)によって返されます。

次の便利なメソッドを使用して、ターゲットの物理および仮想メモリ内の型指定されたデータの読み取りと書き込みを行うことができます。

[**ReadTypedDataPhysical**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-readtypeddataphysical)

[**WriteTypedDataPhysical**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-writetypeddataphysical)

[**ReadTypedDataVirtual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-readtypeddatavirtual)

[**WriteTypedDataVirtual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-writetypeddatavirtual)

### <a name="span-idprinting_typed_dataspanspan-idprinting_typed_dataspanprinting-typed-data"></a><span id="printing_typed_data"></span><span id="PRINTING_TYPED_DATA"></span>型指定されたデータの印刷

型指定されたデータを書式設定して出力コールバックに送信するには、ターゲットの物理メモリと仮想メモリのデータに対して、 [*OutputTypedDataPhysical*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-outputtypeddataphysical)と[*OutputTypedDataVirtual*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-outputtypeddatavirtual)をそれぞれ使用します。

[**DEBUG\_typeopts\_XXX**](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-typeopts-xxx)に記述されている型オプションは、出力コールバックに送信する前に、エンジンが型指定されたデータを書式設定する方法に影響します。

型オプションは、 [**Addtypeoptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-addtypeoptions)を使用して有効にし、 [**removetypeoptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-removetypeoptions)を使用して無効にすることができます。

[**Gettypeoptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-gettypeoptions)は、現在の型のオプションを返します。 すべての型オプションを一度に設定するには、 [**Settypeoptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-settypeoptions)を使用します。

### <a name="span-idinterpreting_raw_data_using_type_informationspanspan-idinterpreting_raw_data_using_type_informationspaninterpreting-raw-data-using-type-information"></a><span id="interpreting_raw_data_using_type_information"></span><span id="INTERPRETING_RAW_DATA_USING_TYPE_INFORMATION"></span>型情報を使用した生データの解釈

デバッガーエンジン API は、型指定されたデータの解釈をサポートしています。 これにより、構造体のメンバーの検索、ポインターの逆参照、配列要素の検索など、ターゲット上のオブジェクト階層を調べることができます。

型指定されたデータは、[**デバッグ\_型指定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_debug_typed_data)された\_データ構造体のインスタンスによって記述され、特定の型へのキャスト先のメモリ領域を表します。 これらのインスタンスを操作するには、型指定された[ **\_データ\_ANSI 要求操作のデバッグ\_要求\_EXT\_** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-request-ext-typed-data-ansi)使用します。 これらは、式の結果に初期化するか、指定した型にメモリの領域をキャストすることによって初期化できます。 ANSI**要求**操作がサポートする\_EXT\_型\_指定された、DEBUG\_要求によってサポートされるすべてのサブ操作の一覧については、「 [**EXT\_tdop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)」を参照してください。\_

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

出力コールバックの詳細については、「[入力と出力](using-input-and-output.md)」を参照してください。

 

 





