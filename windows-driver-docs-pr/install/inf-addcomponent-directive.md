---
title: INF AddComponent ディレクティブ
description: AddComponent ディレクティブにより、現在のデバイスの下にソフトウェアコンポーネントデバイスが作成されます。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 758f80d1d19bb9830b16254d409b9df20ec1cb54
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223202"
---
# <a name="inf-addcomponent-directive"></a>INF AddComponent ディレクティブ

**Addcomponent**ディレクティブは、 [**INF *ddinstall*内で使用されます。**](inf-ddinstall-components-section.md)[拡張機能の INF ファイル](using-an-extension-inf-file.md)の Components セクション。  これにより、現在のデバイスの下にあるソフトウェアコンポーネントの仮想子デバイスが作成されます。 このディレクティブは、Windows 10 バージョン1703以降でサポートされています。 

```inf
[DDInstall.Components]

AddComponent=ComponentName,[flags],component-install-section
```

## <a name="entries"></a>エントリ

*ComponentName*

作成するソフトウェアコンポーネントの名前を指定します。  INF ファイル内の各**Addcomponent**ディレクティブには、一意の値を指定する必要があります。

*flags*

現在未定義ですが、将来使用するために予約されている (論理和) フラグを1つ以上指定します。

*コンポーネント-インストール-セクション*

このデバイスの名前付きソフトウェアコンポーネントを作成するための情報が含まれている INF ライター定義セクションを参照します。  

## <a name="remarks"></a>解説

各 INF ライターで作成されたセクション名は、INF ファイル内で一意である必要があります。また、セクション名を定義するための一般的な規則に従う必要があります。  これらの規則の詳細については、「 [INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)」を参照してください。

**Addcomponent**ディレクティブは、INF ファイル内の別の場所にある、指定された*component-install セクション*を参照する必要があります。  各セクションには、次の形式があります。

```inf
[component-install-section]

ComponentIDs=component-id[,component-id] …
[Description=description]
```

次に示すように、各**ある componentid**には少なくと*も1つ*のエントリが含まれている必要があります。 ただし、残りのエントリは省略可能です。

**ある componentid**はハードウェア[id](hardware-ids.md)であることに注意してください。これは、ハードウェア開発者によって定義された文字列であることを意味します。  これらの Id が一意であることを確認するには、ほとんどの場合、 [PCI デバイス](identifiers-for-pci-devices.md)に使用する識別子スキーマに従うことをお勧めします。  ベンダーは、別のスキーマを使用することもできますが、これはシナリオによって異なります。

たとえば、1つのデバイスに複数のコンポーネントを持つベンダーが、コンポーネントのハードウェア Id を親に関連付けることが必要になる場合があります。  この場合、4文字のベンダー定義のコンポーネント識別子を親のハードウェア ID に追加することによって、 **ComponentID**を作成できます。

## <a name="component-install-section-entries-and-values"></a>コンポーネント-インストールセクションのエントリと値
    
**ある componentid**=*id1 [, id2]...[, idN]*

ソフトウェアコンポーネントのコンポーネント識別子を指定します。  コンポーネント Id は、ハードウェア Id と同じように動作し、[同様のフォーマット](hardware-ids.md)に従う必要があります。 ソフトウェアコンポーネントの場合、システムは INF によって指定され`SWC\`た値の先頭にハードウェア id を作成します。  たとえば、の`VID0001&PID0001` `SWC\VID0001&PID0001`**ある componentid**値がの場合、ハードウェア ID はになります。

**説明**=の*説明*

必要に応じて、ソフトウェアコンポーネント (通常はローカライズ用) を説明する文字列を、 [INF 文字列セクション](inf-strings-section.md)で定義された% strkey% トークンとして指定します。
    
説明文字列に% strkey% トークンが含まれている場合、各トークンは最大511文字を表すことができます。 文字列トークンの置換後の合計文字列は、1024文字を超えないようにする必要があります。

## <a name="see-also"></a>参照

[コンポーネントの INF ファイルを使用](using-a-component-inf-file.md)します。

[*Ddinstall*。**コンポーネント**](inf-ddinstall-components-section.md)

[INF AddSoftware ディレクティブ](inf-addsoftware-directive.md)
