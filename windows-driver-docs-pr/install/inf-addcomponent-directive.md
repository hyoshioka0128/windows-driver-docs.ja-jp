---
title: INF AddComponent ディレクティブ
description: AddComponent、ディレクティブは、現在のデバイスの下にあるソフトウェア コンポーネントのデバイスを作成します。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 71e769c511b985f28a6a9494331e45edfaead520
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383202"
---
# <a name="inf-addcomponent-directive"></a>INF AddComponent ディレクティブ

**AddComponent**内ディレクティブの使用、 [ **INF *DDInstall*します。コンポーネント**](inf-ddinstall-components-section.md)のセクション、[拡張子 INF ファイル](using-an-extension-inf-file.md)します。  現在のデバイスのソフトウェア コンポーネントの子の仮想デバイスを作成します。 Windows 10 バージョン 1703 以降では、このディレクティブはサポートされます。 

```ini
[DDInstall.Components]

AddComponent=ComponentName,[flags],component-install-section
```

## <a name="entries"></a>エントリ

*コンポーネント名*

作成するソフトウェア コンポーネントの名前を指定します。  各**AddComponent** INF ファイルのディレクティブは値が一意である必要があります。

*flags*

現在定義されていませんが、予約済みなど、1 つまたは複数の (論理和) フラグを指定します。

*component-install-section*

このデバイスの名前付きのソフトウェア コンポーネントを作成するための情報を含む INF ライター定義のセクションを参照します。  

## <a name="remarks"></a>コメント

各 INF ライター作成セクション名は、INF ファイル内で一意である必要があり、セクション名を定義するための一般的な規則に従う必要があります。  これらの規則の詳細については、次を参照してください。 [INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)します。

**AddComponent**ディレクティブは名前付き参照する必要があります*コンポーネントのインストール-セクション*INF ファイルで別の場所。  このような各セクションでは、次の形式があります。

```ini
[component-install-section]

ComponentIDs=component-id[,component-id] …
[Description=description]
```

各*コンポーネントのインストール-セクション*必要があります、少なくとも**componentid が**次に示すように入力します。 ただし、残りのエントリは省略可能です。

なお**componentid が**は[HardwareIDs](hardware-ids.md)、ハードウェア開発者によって定義された文字列はことを意味します。  一意性を確保するこれらの Id、ほとんどの場合推奨するのに使用される識別子スキーマ[PCI デバイス](identifiers-for-pci-devices.md)します。  別のスキーマを使用する仕入先が、シナリオによって異なります。

たとえば、1 つのデバイス上の複数のコンポーネントと仕入先は、ハードウェア コンポーネントの Id を関連付ける親する可能性があります。  この場合、作成できます、 **ComponentID** 4 文字のベンダ定義のコンポーネントの識別子、親のハードウェア ID を追加することで。

## <a name="component-install-section-entries-and-values"></a>コンポーネントのインストール」セクションのエントリと値
    
**ComponentIDs**=*id1[, id2] … [, idN]*

ソフトウェア コンポーネントのコンポーネントの識別子を指定します。  コンポーネント Id が、同じ動作方法するハードウェア Id これを行うと、従う必要があります[のような書式設定](hardware-ids.md)します。 ソフトウェア コンポーネントは、システムは INF が指定した値を付加`SWC\`ハードウェア Id を作成します。  たとえば、 **componentid が**の値`VID0001&PID0001`結果のハードウェア ID、`SWC\VID0001&PID0001`します。

**説明**=*の説明*

必要に応じて で定義されている %strkey% トークンとして表される、ローカライズの通常のソフトウェアのコンポーネントを説明する文字列を指定します、 [INF 文字列セクション](inf-strings-section.md)します。
    
説明の文字列に %strkey% のすべてのトークンが含まれている場合、各トークンは、最大 511 文字を表すことができます。 合計の文字列では、文字列トークン置換後にする必要がありますは 1024 文字以下。

## <a name="see-also"></a>関連項目

[コンポーネントの INF ファイルを使用して](using-a-component-inf-file.md)します。

[*DDInstall*.**コンポーネント**](inf-ddinstall-components-section.md)

[INF AddSoftware ディレクティブ](inf-addsoftware-directive.md)
