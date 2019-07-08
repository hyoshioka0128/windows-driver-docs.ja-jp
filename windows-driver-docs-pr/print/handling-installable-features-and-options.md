---
title: インストール可能な機能とオプションの処理
description: インストール可能な機能とオプションの処理
ms.assetid: b970808f-55bd-4a3a-9464-c9cd3567fa6f
keywords:
- Unidrv、インストール可能な機能とオプション
- インストール可能な機能とオプション WDK Unidrv
- GPD は、WDK Unidrv、インストール可能な機能とオプションのファイルします。
- Unidrv WDK の印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e470708dcfba3f2b5ef7256eecf36f574faa170
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360536"
---
# <a name="handling-installable-features-and-options"></a>インストール可能な機能とオプションの処理





プリンターの機能やオプションの一部は、インストール可能な可能性があります。 たとえば、プリンター可能性がありますか、現在接続できませんが、省略可能な封筒フィーダーを受け入れることでした。 2 つの方法で GPD ファイル内でこの封筒フィーダーに記述する必要があります。

-   として InputBin 機能のオプションです。

-   インストール可能な「機能」として (にもかかわらずは本当にオプション)、ユーザーが実際にインストールされているかどうかを示すことができます。

最初に、InputBin 機能のオプションとして、自動のフィーダーと共に、封筒フィーダーを指定する、次の GPD エントリされる可能性があります。

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

封筒フィーダーをインストールするためには、追加 GPD エントリが必要なとしては、次のようにします。

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

内で、\*エントリのオプション [封筒フィーダー] に、2 つの属性が追加されました。

-   \*インストール可能でしょうか。 属性は、オプションがインストール可能であることを示します。

-   \*InstallableFeatureName 属性 Unidrv ができるように、ユーザーは、オプションが実際にインストールされているかどうかを示すことができますを表示するテキスト文字列を指定します。

たびに **\*インストール可能ですか?** に設定されている **TRUE** Unidrv 機能またはオプションでは、プロパティ シートの表示の追加機能を作成します。 (いる場合でも、インストール可能な項目は、オプションは、Unidrv 表現を作成します機能のプロパティ シートに注意してください)。この Unidrv 合成機能がで指定された文字列で識別される **\*InstallableFeatureName**します。 機能は、「インストール済み」と「インストールされていない」、2 つのオプションを提供し、これらのオプションのいずれかを選択できます。 文字列「インストール」と「インストールされていません」がで指定された、 \*InstalledOptionName と\*NotInstalledOptionName 属性の他のテキストがより適切な場合は変更できるようにします。

したがって、この例では、プロパティ シートは、InputBin 機能を含めますが、ラベル付け**入力ビン**、というラベルの付いた 2 つのオプションを含む**自動フィーダー**と**封筒フィーダー**. プロパティ シートは、ラベル付け、追加機能も含まれます**オプションの封筒フィーダー**、2 つのオプションというラベルの付いた**インストール済み**と**インストールされていない**。 ユーザーが選択できるだけ**封筒フィーダー** **入力ビン**勝負を最初に選択した場合**インストール済み** **封筒フィーダーが省略可能な**.

場合によっては、特定のインストール可能なオプションを同時にインストールできないことや、インストール可能なその他のいくつかのオプションがインストールされている場合に、特定 noninstallable オプションを選択できないことを指定する必要があります。 このような状況を処理するために使用を指定する GPD エントリ[制約オプション](option-constraints.md)します。

使用することはできません、\*インストール可能でしょうか。 必要とする省略可能な機能を持つ属性を\*DisabledFeatures エントリ。 これらの機能では、「インストール」と「インストールされていない」オプションで、省略可能な機能を明示的に指定する必要があります。 たとえば、プリンターに、オプションの両面印刷ユニットがあるとします。 双方向機能 (を参照してください[標準機能](standard-features.md))、両面印刷ユニットがインストールされていない場合、無効にする必要があります。 「インストール済み」と「インストールされていません」のオプションを使用して、「オプションの両面印刷ユニット」機能を定義する必要があります。 内の「インストールされていない」\*含めますオプションのエントリを\*DisabledFeatures 双方向機能のエントリ。 次の GPD エントリを使用できます。

```cpp
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

また、関連するすべて指定してください[制約オプション](option-constraints.md)ように。

 

 




