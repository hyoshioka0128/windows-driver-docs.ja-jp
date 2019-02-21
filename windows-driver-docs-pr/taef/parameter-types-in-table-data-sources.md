---
title: パラメーター テーブルのデータ ソースの型
description: パラメーター テーブルのデータ ソースの型
ms.assetid: 034F171E-716F-4795-9B07-46A109052227
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3004599456191567616a82ae54546f5ac447f59
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529409"
---
# <a name="parameter-types-in-table-data-sources"></a>パラメーター テーブルのデータ ソースの型


次の表には、概要テーブルで使用できるさまざまなパラメーターの型のベースのデータ ソースとどの型文字列を使用して互換性のあるデータ ソース ファイルにすることができます、ネイティブで管理され、スクリプトをテストします。

ネイティブ管理スクリプト ParameterType LanguageType ParameterType LanguageType ParameterType LanguageType"String"WEX::Common::String"String"の文字列"String"または"BSTR"VT\_BSTR"int"int"Int32"または"int"int"int"VT\_INT"unsigned int"unsigned int"uint"または"uint32"uint"unsigned int"または"uint"VT\_UINT"bool"bool"bool"または"boolean"bool"bool"VT\_BOOL"double"double"double"または"decimal"decimal"double"VT\_R8"\_\_int64" \_ \_int64"\_\_int64"または"int64"int64"\_\_int64"VT\_I8"符号なし\_ \_int64"符号なし\_ \_int64"符号なし\_ \_int64"または"uint64"uint64"符号なし\_ \_int64"VT\_UI8"DWORD"DWORD"DWORD"uint"サイズ\_t"サイズ\_t"NoThrowString"WEX::Common::NoThrowString"XML"WEX::Common::String"XML"文字列"XML"VT\_BSTR
 

注: "String"、"int"、"bool"、"double"、"\_\_int64"、"符号なし\_ \_int64"、"XML"の種類を使用して、すべての管理、ネイティブまたはスクリプトをテストします。

既定では、型が指定されていない場合、型と見なされます"String"にします。 上記の最初の行を参照してください。

上記で指定した任意のタイプを合わせて配列型を指定するだけ追加"\[\]"型の末尾にします。

 

 





