---
title: インストール可能な機能とオプションの処理
description: インストール可能な機能とオプションの処理
ms.assetid: b970808f-55bd-4a3a-9464-c9cd3567fa6f
keywords:
- Unidrv、インストール可能な機能、およびオプション
- インストール可能な機能とオプション WDK Unidrv
- GPD files WDK Unidrv、インストール可能な機能およびオプション
- Unidrv WDK 印刷
ms.date: 06/09/2020
ms.localizationpriority: medium
ms.openlocfilehash: d9bc895385a652bc7f3f5f1c036b084eef0bb326
ms.sourcegitcommit: 88f6e7355de9e0714057020557dc8c7831e90e7b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/10/2020
ms.locfileid: "84638440"
---
# <a name="handling-installable-features-and-options"></a>インストール可能な機能とオプションの処理

プリンターの機能の中には、インストール可能なものもあります。 たとえば、プリンターはオプションの封筒フィーダーを受け入れることができますが、これは現在接続されていない可能性があります。 この封筒フィーダーは、次の2つの方法で GPD ファイル内に記述する必要があります。

- InputBin 機能のオプションとして。

- インストール可能な "機能" として (実際にはオプションですが)、ユーザーが実際にインストールされているかどうかを示すことができます。

まず、InputBin 機能のオプションとして封筒フィーダーと自動フィーダーを指定するには、次の GPD エントリを使用できます。

```cpp
*Feature: InputBin
{
    *Name: "Input Bin"
    *Option: AUTO
    {
        *Name: "Automatic Feeder"
        *Command: CmdSelect {Command Attributes}
    }
    *Option: ENVFEED
    {
        *Name: "Envelope Feeder"
        *Command: CmdSelect {Command Attributes}
    }
}
```

封筒フィーダーをインストールできるようにするには、次のように、追加の GPD エントリが必要になります。

```cpp
*InstalledOptionName: "Installed"
*NotInstalledOptionName: "Not installed"
*Feature: InputBin
{
    *Name: "Input Bin"
    *Option: AUTO
    {
        *Name: "Automatic Feeder"
        *Command: CmdSelect {Command Attributes}
    }
    *Option: ENVFEED
    {
        *Name: "Envelope Feeder"
        *Command: CmdSelect {Command Attributes}
        *Installable?: TRUE
        *InstallableFeatureName: "Optional Envelope Feeder"
    }
}
```

\*封筒フィーダーのオプションエントリ内には、次の2つの属性が追加されています。

- \*インストール可能な属性は、オプションがインストール可能であることを示します。

- InstallableFeatureName 属性では、 \* オプションが実際にインストールされているかどうかをユーザーが示すことができるように、Unidrv に表示されるテキスト文字列を指定します。

** \* インストール可能**な場合はいつでも、機能またはオプションの [ **TRUE** ] に設定されています。 Unidrv を使用すると、プロパティシートの表示用の追加機能が作成されます。 (インストール可能な項目がオプションの場合でも、Unidrv はプロパティシートにその機能の表現を作成します)。この Unidrv 合成機能は、 ** \* InstallableFeatureName**で提供される文字列によって識別されます。 この機能には、"インストール済み" と "未インストール" の2つのオプションが用意されており、ユーザーはこれらのオプションのいずれかを選択できます。 "Installed" および "Not installed" という文字列は、 \* \* 他のテキストがより適切である場合に変更できるように、InstalledOptionName 属性と NotInstalledOptionName 属性で指定します。

そのため、この例では、プロパティシートに " **Input bin**" というラベルが付いた inputbin 機能が含まれています。この機能には、**自動フィーダー**と**封筒フィーダー**というラベルが付いた2つのオプションがあります。 プロパティシートには、**オプションのエンベロープフィーダー**というラベルが付いた追加機能も含まれており、2つのオプションが**インストール**されており、インストールされて**いません**。 ユーザーは、[**入力ビン**] の下にある [**封筒フィーダー** ] を選択できます **(オプションの封筒フィーダー**で [**インストール済み**] を選択した場合のみ)。

場合によっては、インストール可能な特定のオプションを同時にインストールできないこと、または他のインストール可能なオプションがインストールされている場合は、インストールされていない特定のオプションを選択できないことを示す必要があります。 このような状況に対処するには、[オプション制約](option-constraints.md)を指定する GPD エントリを使用します。

\*DisabledFeatures エントリを必要とするオプション機能では、インストール可能な? 属性を使用できません \* 。 これらの機能については、オプションの機能を明示的に指定し、[インストール済み] と [未インストール] のオプションを指定する必要があります。 たとえば、プリンターにオプションの二重単位があるとします。 両面印刷装置がインストールされていない場合は、二重機能 (「[標準機能](standard-features.md)」を参照) を無効にする必要があります。 "インストール済み" と "未インストール" のオプションを使用して、"オプションの二重単位" 機能を定義する必要があります。 "インストールされていません" オプションのエントリ内には、 \* \* 二重機能の DisabledFeatures エントリが含まれます。 次の GPD エントリを使用できます。

```console
*Feature: DuplexUnit
{
    *ConflictPriority: 3   *% Make priority higher than Duplex feature
    *Name: "Optional Duplexing Unit"
    *Option: Installed
    {
        *Name: "Installed"
    }
    *Option: NotInstalled
    {
        *Name: "Not Installed"
        *DisabledFeatures: LIST(Duplex)
        *Constraints: LIST (Duplex.LongEdge, Duplex.ShortEdge)
    }
}
```

図に示すように、関連する[オプション制約](option-constraints.md)も指定してください。
