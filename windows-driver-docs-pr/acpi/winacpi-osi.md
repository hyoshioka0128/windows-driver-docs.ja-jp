---
title: _OSI を使用して ACPI で Windows バージョンを識別する方法
description: ホスト オペレーティング システムの識別に使用される ACPI ソース言語 (ASL) のオペレーティング システム インターフェイス レベル (\_OSI) メソッドについて説明します。
ms.date: 04/14/2020
ms.localizationpriority: medium
ms.openlocfilehash: 4602a8fc145d9b64d5bf163f5aa46aa9900e1a81
ms.sourcegitcommit: 958a5ced83856df22627c06eb42c9524dd547906
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83235370"
---
# <a name="how-to-identify-the-windows-version-in-acpi-by-using-_osi"></a>_OSI を使用して ACPI で Windows バージョンを識別する方法

このトピックでは、 \_ Advanced Configuration And Power Interface (ACPI) ソース言語 (ASL) で OSI メソッドを使用して、ホストオペレーティングシステムを識別する方法について説明します。 この方法を使用すると、ASL ライターは、将来のオペレーティングシステムのバージョンをサポートするファームウェアを作成し、要求されたインターフェイスレベルに基づいてオペレーティングシステムが動作を変更できるようになります。

この情報は、次のオペレーティングシステムに適用されます。

- Windows 10 バージョン2004
- Windows 10 バージョン 1903
- Windows 10 Version 1809
- Windows 10 バージョン 1803
- Windows 10 バージョン 1709
- Windows 10 Version 1703
- Windows 10 Version 1607
- Windows Server Technical Preview
- Windows 10
- Windows Server 2012 R2
- Windows 8.1
- Windows Server 2012
- Windows 8
- Windows Server 2008 R2
- Windows 7
- Windows Server 2008
- Windows Vista
- Windows Server 2003
- Windows XP

## <a name="the-_osi-method"></a>\_OSI メソッド

Windows オペレーティングシステムの最近のバージョンはすべて、 [Advanced Configuration And Power Interface (ACPI) 仕様](https://uefi.org/specifications)のコンポーネントをサポートしています。 ACPI 仕様では、解釈された言語である ACPI ソース言語 (ASL) を定義します。これにより、オペレーティングシステムは、電源管理と構成について、ファームウェアによって提供される制御方法を実行できます。 ASL ライターがホストオペレーティングシステムのバージョンを識別する機能を向上させるために、ASL にはオペレーティングシステムインターフェイスレベル (OSI) が用意されて \_ います。

ASL ライターは、OSI メソッドを使用して、 \_ ホストオペレーティングシステムがサポートする ACPI インターフェイスのバージョンを簡単に判別できます。 このバージョン管理方法は、将来のオペレーティングシステムをサポートするファームウェアを作成し、要求されたインターフェイスレベルに基づいてオペレーティングシステムが動作を変更できるようにするためのソリューションを提供します。

## <a name="_osi-defined"></a>\_定義済みの OSI

\_OSI メソッドには、1つの引数と1つの戻り値があります。 引数は、各オペレーティングシステムに対して定義される文字列です。 インターフェイスがサポートされていない場合、戻り値は0x00000000、インターフェイスがサポートされている場合は0xFFFFFFFF です。

ACPI 仕様の最近のバージョンでは、 \_ ホストオペレーティングシステムのバージョン識別以外に、OSI メソッドのユースケースが拡張されています。 ただし、Windows で \_ は、システムで実行されている windows のホストバージョンを識別するためにのみ、OSI がサポートされます。

OSI メソッドは次のように \_ 定義されています。

- \\\_OSI-オペレーティングシステムインターフェイス

### <a name="argument"></a>引数

各オペレーティングシステムに対して定義された文字列。 次に例を示します。

- Windows 8.1 および Windows Server 2012 R2 の場合は "windows 2013"
- Windows 8 および Windows Server 2012 の場合は "windows 2012"
- Windows 7 および Windows Server 2008 R2 の場合は "windows 2009"
- Windows XP の場合は "windows 2001"
- Windows Server 2003 の場合は "windows 2001.1"

### <a name="return-value"></a>戻り値

戻り値は次のとおりです。

- オペレーティングシステムが引数のバージョンをサポートしていない場合は0x00000000。
- オペレーティングシステムが引数のバージョンをサポートしている場合は0xFFFFFFFF。

## <a name="_osi-argument-details-for-windows"></a>\_Windows の OSI 引数の詳細

次の表は、対応する OSI 文字列を使用して ASL が識別できる Windows のバージョンを示して \_ います。

Windows オペレーティングシステムでは、OSI メソッドの引数によって \_ 以前のバージョンの Windows が指定されている場合、0xffffffff が返されます。 たとえば、Windows 7 では、"Windows 2009" (Windows 7) と "Windows 2006" (Windows Vista) の両方に対して0xFFFFFFFF が返されます。

### <a name="_osi-strings-for-windows-operating-systems"></a>\_Windows オペレーティングシステム用の OSI 文字列

| OSI 文字列          | 対象 OS                     |
|---------------------|-------------------------------|
| Windows 2000        | Windows 2000                  |
| Windows 2001        | Windows XP                    |
| Windows 2001 SP1    | Windows XP SP1                |
| Windows 2001.1      | Windows Server 2003           |
| Windows 2001 SP2    | Windows XP SP2                |
| Windows 2001.1 SP1  | Windows Server 2003 SP1       |
| Windows 2006        | Windows Vista                 |
| Windows 2006 SP1    | Windows Vista SP1             |
| Windows 2006.1      | Windows Server 2008           |
| Windows 2009        | Windows 7、Win Server 2008 R2 |
| Windows 2012        | Windows 8、Win Server 2012    |
| Windows 2013        | Windows 8.1                   |
| Windows 2015        | Windows 10                    |
| Windows 2016        | Windows 10 Version 1607      |
| Windows 2017        | Windows 10 Version 1703      |
| Windows 2017.2      | Windows 10 バージョン 1709      |
| Windows 2018        | Windows 10 バージョン 1803      |
| Windows 2018.2      | Windows 10 Version 1809      |
| Windows 2019        | Windows 10 バージョン 1903      |
| Windows 2020        | Windows 10 バージョン2004      |

### <a name="implementation-note"></a>実装に関する注意

オペレーティングシステムを識別するルーチンを SB スコープの下にある INI メソッドに配置して、 \_ \\ \_ \_ OSI ができるだけ早く実行されるようにします。 この配置は、オペレーティングシステムによって、OSI メソッドの文字列引数に基づいて機能が利用可能になるため、重要です \_ 。

## <a name="additional-resources"></a>その他のリソース

[高度な構成と電源インターフェイスの仕様](https://uefi.org/specifications)
