---
title: _OSI を使用して ACPI で Windows バージョンを識別する方法
description: ホスト オペレーティング システムの識別に使用される ACPI ソース言語 (ASL) のオペレーティング システム インターフェイス レベル (\_OSI) メソッドについて説明します。
ms.date: 11/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: c25144a88437574a1aae4b762e7a459b09637c88
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355798"
---
# <a name="how-to-identify-the-windows-version-in-acpi-by-using-osi"></a>_OSI を使用して ACPI で Windows バージョンを識別する方法

このトピックでは、使用する方法を説明します、 \_OSI メソッドで、ホスト オペレーティング システムを識別するために Advanced Configuration and Power Interface (ACPI) ソース言語 (ASL)。 このメソッドを使用すると、ASL ライターは、ファームウェアを将来のオペレーティング システムのバージョンをサポートし、により、要求されたインターフェイスのレベルに基づく動作を変更するオペレーティング システムを作成できます。

この情報は、次のオペレーティング システムに適用されます。

- Windows 10 Version 1809
- Windows 10 バージョン 1803
- Windows 10 バージョン 1709
- Windows 10 Version 1703
- Windows 10 Version 1607
- Windows Server Technical Preview
- Windows 10
- Windows Server 2012 R2
- Windows 8.1
- Windows Server 2012
- Windows 8
- Windows Server 2008 R2
- Windows 7
- Windows Server 2008
- Windows Vista
- Windows Server 2003
- Windows XP

## <a name="the-osi-method"></a>\_OSI メソッド

Windows オペレーティング システムのすべての最新バージョンのコンポーネントをサポートする、 [Advanced Configuration and Power Interface (ACPI) 仕様](https://uefi.org/specifications)します。 ACPI の仕様には、ACPI ソース言語 (ASL)、電源管理と構成のファームウェアで提供されるコントロールのメソッドを実行するオペレーティング システムを有効にする、インタープリター言語が定義されています。 ホスト オペレーティング システムのバージョンを識別するために ASL ライターの機能を向上させるのには、ASL はオペレーティング システム インターフェイス レベルを提供します。 (\_OSI)。

使用して、 \_OSI メソッド、ASL ライターは、ホスト オペレーティング システムをサポートする ACPI インターフェイスのバージョンを確認する簡単にします。 このバージョン管理メソッドでは、将来のオペレーティング システムをサポートでき、要求されたインターフェイスのレベルに基づく動作を変更するオペレーティング システムを有効にしているファームウェアを作成するため、ソリューションを提供します。

## <a name="osi-defined"></a>\_OSI の定義

\_OSI メソッドが 1 つの引数と戻り値の 1 つの値。 引数は、およびオペレーティング システムごとに定義する文字列です。 戻り値は、インターフェイスがサポートされている場合は、インターフェイスがサポートされていない場合は 0x00000000 または 0 xffffffff です。

最近のバージョン、ACPI 仕様の拡張のユース ケース、\_ホスト オペレーティング システムのバージョン番号を超える OSI メソッド。 ただし、Windows がサポートしている\_OSI システムで実行されている Windows のホスト バージョンを識別するの使用するためだけです。

\_OSI メソッドは次のように定義されます。

- \\\_OSI - オペレーティング システムのインターフェイス

### <a name="argument"></a>引数

各オペレーティング システムで定義された文字列。 例:

- 「Windows 2013」for Windows 8.1 および Windows Server 2012 R2
- Windows 8 および Windows Server 2012 の「Windows 2012」
- Windows 7 の「Windows 2009」と Windows Server 2008 R2
- Windows XP の「2001 年の Windows」
- Windows Server 2003 の「Windows 2001.1」

### <a name="return-value"></a>戻り値

戻り値は次のとおりです。

- オペレーティング システムは、引数のバージョンをサポートしていない場合は 0x00000000 します。
- オペレーティング システムは、引数のバージョンをサポートしている場合に 0 xffffffff です。

## <a name="osi-argument-details-for-windows"></a>\_Windows の OSI 引数の詳細

次の表は、対応するを使用して ASL を識別する Windows のバージョンを示します\_OSI 文字列。

Windows オペレーティング システムが 0 xffffffff を返す場合に引数、 \_OSI メソッドは、Windows の以前のバージョンを指定します。 たとえば、Windows 7 には、0 xffffffff の両方"Windows 2009"(Windows 7) と「Windows 2006」(Windows Vista) が返されます。

**\_Windows オペレーティング システムの OSI 文字列**

| OSI 文字列          | 対象 OS                     |
|---------------------|-------------------------------|
| Windows 2000        | Windows 2000                  |
| Windows 2001        | Windows XP                    |
| Windows 2001 SP1    | Windows XP SP1                |
| Windows 2001.1      | Windows Server 2003           |
| Windows 2001 SP2    | Windows XP SP2                |
| Windows 2001.1 SP1  | Windows Server 2003 SP1       |
| Windows 2006        | Windows Vista                 |
| Windows 2006 SP1    | Windows Vista SP1             |
| Windows 2006.1      | Windows Server 2008           |
| Windows 2009        | Windows 7、Win Server 2008 R2 |
| Windows 2012        | Windows 8 を Win Server 2012    |
| Windows 2013        | Windows 8.1                   |
| Windows 2015        | Windows 10                    |
| Windows 2016        | Windows 10 Version 1607      |
| Windows 2017        | Windows 10 Version 1703      |
| Windows 2017.2      | Windows 10 バージョン 1709      |
| Windows 2018        | Windows 10 バージョン 1803      |
| Windows 2018.2      | Windows 10 Version 1809      |

### <a name="implementation-note"></a>実装に注意してください。

オペレーティング システムを識別するルーチンを配置、 \_INI メソッドの下、 \\ \_SB スコープように\_OSI をできるだけ早く実行できます。 この配置は、オペレーティング システムでは、使用可能な機能への文字列引数に基づくために、重要な\_OSI メソッド。

## <a name="additional-resources"></a>その他の資料
[Advanced Configuration and Power Interface Specification](https://uefi.org/specifications)
