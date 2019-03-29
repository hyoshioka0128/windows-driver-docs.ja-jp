---
title: V_NET_ROOT 構造
description: V_NET_ROOT 構造
ms.assetid: 866eba91-13b6-4b15-93de-4f627a635c92
keywords:
- WDK RDBSS のマッピングを共有します。
- V_NET_ROOT 構造 WDK RDBSS
- 共有のマッピング
- データ構造体の WDK ファイル システム
- RDBSS WDK ファイル システム、接続およびファイル構造
- リダイレクトされたサブシステムの WDK のバッファリングをドライブのファイル システム、接続およびファイル構造
- 接続が WDK RDBSS 構造体します。
- ファイル構造 WDK RDBSS
- WDK RDBSS 構造体
- WDK RDBSS の接続情報
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ea8c7fd4a396b21a531003e8f6576b160302b4c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573362"
---
# <a name="the-vnetroot-structure"></a>V\_NET\_ルート構造体


## <span id="ddk_the_v_net_root_structure_if"></span><span id="DDK_THE_V_NET_ROOT_STRUCTURE_IF"></span>


V\_NET\_ルート構造体は、共有 (たとえば、ユーザー ドライブ マッピングを関連付けられている共有ポイントのルートの下に示す) にマッピングするためのメカニズムを提供します。 V\_NET\_ルート名は、次の形式のいずれかで指定できます。

```cpp
\server\share\d1\d2
\;m:\server\share\d1\d2
```

名前の形式に依存この V に関連付けられているローカル デバイス (「x:」、たとえば) があるかどうか\_NET\_ルート構造体。 ローカル ドライブのマッピングの場合 (d1\\例については、d2)、ローカル ドライブ マッピングが各にプレフィックスを取得[ **CreateFile** ](https://msdn.microsoft.com/library/windows/desktop/aa363858)この V の開いている\_NET\_ルート構造体。

V\_NET\_資格情報を指定するルート構造体にも使用します。 このような V の目的は、\_NET\_ルート構造体は、NET に代替の資格情報を伝達する\_ルートの既定値。 このため、必要がありますいないその他の参照。

V の一覧\_NET\_RDBSS によって各ネットワークのルート構造体が保持される\_ルート。 各 V\_NET\_ルート構造が V に固有の要素と共に、他の RDBSS 構造と一般的ないくつかの要素を持つ\_NET\_ルート構造体。 V を管理する RDBSS ルーチン\_NET\_ルート構造体は、次の要素のみを変更します。

-   署名と参照カウント

-   関連付けられているネットワークへのポインター\_ルート構造体とのリンク

-   テーブルの検索 (プレフィックス) の名前の情報

-   名前、ユーザーを追加するプレフィックスの名前が表示されます (これは、NET をシミュレートするため\_実際 NET のルートにマップされていないルート構造\_ルート構造体)

V のファイナライズ\_NET\_ルート構造は、2 つの部分で構成されます。

1.  すべての SRV との関連付けを破棄する\_オープン構造体

2.  メモリの解放

これら 2 つのアクションと V 内のフィールド間に遅延があります\_NET\_ルート構造体から重複する最初の手順をできないようにします。

 

 




