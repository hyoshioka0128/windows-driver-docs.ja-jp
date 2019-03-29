---
title: HelpText 値の追加
description: HelpText 値の追加
ms.assetid: fb29852c-5d47-4660-9fe4-dc8ae05449ff
keywords:
- 追加レジストリ セクション WDK ネットワー キング、HelpText 値
- HelpText 値 WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0573a425ae6b2f68cff26c78b40c2f5fbaa18be
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570748"
---
# <a name="adding-a-helptext-value"></a>HelpText 値の追加





INF ファイルを**NetTrans**、 **NetClient**、または**NetService**ユーザー インターフェイスに表示されているネットワーク コンポーネントを追加する必要があります、 **HelpText**値 (REG\_SZ) をコンポーネントの**Ndi**キー。

**注**  **NetClient**コンポーネントは Windows 8.1、Windows Server 2012 R2 で非推奨以降。

 

**HelpText**値がローカライズ可能な文字列をコンポーネントでのユーザーの利点を説明します。 など、 **HelpText**の値を**NetClient**コンポーネントを持たないクライアントを識別するだけですが、クライアントの使用への接続にユーザーを示します。 **HelpText**の下部にある値が表示されます、**全般**のページ、**接続プロパティ**と、ページ上のコンポーネント ダイアログ ボックスが選択されています。

**注**  Net コンポーネント (アダプター) および IrDA コンポーネントはサポートされず、 **HelpText**値。

 

例を次に、*追加レジストリ セクション*を追加する、 **HelpText**値を**Ndi**キー。

```INF
[MS_Protocol.ndi_reg]
HKR, Ndi, HelpText, 0, %MyTransport_Help%
```

**HelpText**値は、% *strkey*% トークンで定義されている、**文字列**INF ファイルのセクション。 詳細については、**文字列**セクションを参照してください、 [ **INF 文字列セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547485)します。

**注**  Multilingual User Interface (MUI) のサポート、 **HelpText**値に間接的な文字列形式を指定できます`@filename,resource`します。 例:"@% SystemRoot %\\System32\\ドライバー\\mydriver.sys、-1000"。 対象の文字列は、指定したファイルにあります。 リソースの値は、ファイル内の特定の文字列を識別します。 リソースの値が 0 の場合、数は、バイナリ ファイル内の文字列のインデックスとして使用されます。 リソースの値が負の場合、リソース ファイル内のリソース識別子として使用します。

 

 

 





