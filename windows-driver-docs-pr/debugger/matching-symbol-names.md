---
title: シンボル名の照合
description: シンボル名の照合
ms.assetid: 34e2401e-9074-4adc-9644-48ad768c7c2f
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ec0923b8195cba2142965c877a8d3302c4ade84
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571507"
---
# <a name="matching-symbol-names"></a>シンボル名の照合


特定の状況では、シンボルの実際の名前は問題に一致するシンボルになることができますし、別の形式に置き換えられます。 このほとんどは、パブリックおよびプライベート シンボルの間で変更する場合、または MS-DOS 互換の 8.3 のファイルの短い名前を使用する場合によく発生します。

### <a name="span-idpublicvsprivatesymbolmatchingspanspan-idpublicvsprivatesymbolmatchingspanpublic-vs-private-symbol-matching"></a><span id="public_vs__private_symbol_matching"></span><span id="PUBLIC_VS__PRIVATE_SYMBOL_MATCHING"></span>パブリックとします。一致するプライベート シンボル

パブリック シンボルとプライベート シンボルを切り替えると、問題に一致するシンボルを原因場合があります。 通常、パブリック シンボルと、対応するプライベート シンボルは、異なるシンボルの装飾で同じ名前を指定します。 場合によっては、まったく別の名前があります。 このような場合は、両方の名前を明示的に参照する必要があります。 たとえば、2 つのブレークポイントを設定する可能性があります: パブリックのシンボルとプライベート シンボルのもう 1 つ。 詳細については、次を参照してください。[パブリックおよびプライベート シンボルの](public-and-private-symbols.md)します。

### <a name="span-idmsdoscompatability83shortnamesymbolmatchingspanspan-idmsdoscompatability83shortnamesymbolmatchingspanms-dos-compatibility-83-short-name-symbol-matching"></a><span id="ms_dos_compatability_8_3_short_name_symbol_matching"></span><span id="MS_DOS_COMPATABILITY_8_3_SHORT_NAME_SYMBOL_MATCHING"></span>MS-DOS 互換の 8.3 の短い名前一致するシンボル

非常に長い名前を持つファイルが MS-DOS 互換の 8.3 短い名前を自動生成された指定されたことがあります。 ツールとデバッグ、シンボル ファイルを作成するために使用するオプションに応じて、イメージのデバッグ レコードに格納されているファイル名は、長い名前またはこれらの短い名前の 1 つすることができます。 短い名前を使用すると、これとシンボルが割り当てられている短い名前はシステムによって異なりますので問題に一致する可能性があります。

たとえば、Longfilename1.pdb と Longfilename2.pdb の 2 つのファイルがあるとします。 れたりするだと同じディレクトリに Longfi~1.pdb の MS-DOS 互換の 8.3 名を 1 つがもう Longfi~2.pdb になります。 同じディレクトリに配置されない場合両方される Longfi~1.pdb します。 したがって、関連付けられた .pdb ファイルは、不注意コピーは、短いファイル名は変更できます、問題に一致するシンボルの原因です。 詳細については、次を参照してください。[ファイル システムの参照とシンボル ファイル](file-system-references-and-symbol-files.md)します。

 

 





