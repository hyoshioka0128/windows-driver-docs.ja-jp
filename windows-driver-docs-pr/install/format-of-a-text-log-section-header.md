---
title: テキスト ログ セクション ヘッダーの書式
description: テキスト ログ セクション ヘッダーの書式
ms.assetid: ec46a540-e888-426d-85fc-6ad2d756c7b8
keywords:
- セクション ヘッダーの WDK SetupAPI ログ記録
- WDK SetupAPI ログ出力を書式設定します。
- テキスト ログの WDK SetupAPI、セクション ヘッダー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1802e4caf2a7998bc557004201e9756eb311a745
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377072"
---
# <a name="format-of-a-text-log-section-header"></a>テキスト ログ セクション ヘッダーの書式


A*テキスト ログ セクション ヘッダー*の 2 つのログ エントリで構成されます。 最初のエントリの形式が含まれています、"&gt; &gt; &gt; "プレフィックス文字列に続けて、 *section_title*フィールドおよび*instance_identifier*フィールド。 次の例では、斜体のフォント スタイル内のテキスト セクションの作成者が指定されているセクション固有のテキストのプレース ホルダーは、太字のフォントのスタイル内のテキストは、SetupAPI によって提供されるログ記録します。

```cpp
>>>  [section_title - instance_identifier] 
```

*Section_title*フィールドは常に存在し、セクションに関連付けられている操作のタイトルを提供します。

*Instance_identifier*理想的には、一意には、操作のインスタンスを識別する識別子を提供します。 場合、 *instance_identifier*フィールドが存在しない、セクション ヘッダーの最初のエントリの形式は次のようには。

```cpp
>>>  [section_title] 
```

セクション ヘッダーの 2 番目のエントリの形式が含まれています、"&gt; &gt; &gt; "プレフィックス文字列に続けて、 *time_stamp*フィールドと「セクション スタート」を文字列、次のように。

```cpp
>>>  time_stamp Section start
```

形式、 *time_stamp*フィールドを次に示します。

```cpp
yyyy/mm/dd hh:mm:ss.sss:
```

場所、 *time_stamp*サブフィールドは、次のとおり。

-   *yyyy*は 4 桁の年、 *mm*は 2 桁の月、および*dd*は 2 桁の日です

-   ローカル時刻が、24 時間制に基づいて、 *hh*は 2 桁の時、 *mm*は 2 桁の分単位では、 *ss* 2 桁の秒数は、sss は 3 桁の数字の数(ミリ秒)。

次は、PCI デバイスのインストール操作をグループにユーザー モードのプラグ アンド プレイ (PnP) マネージャーを作成する一般的なセクション ヘッダーの例です。 *Section_title*フィールドは「デバイスをインストールする」、 *instance_identifier*フィールドは、デバイスのインスタンス識別子"PCI\\VEN_104C & DEV_8019 & SUBSYS_8010104C REV_00\\3 & 61aaa01 & 0 & 38 で、"および*time_stamp*フィールドが"2005/02/13 22:06:28.109:."

```cpp
>>>  [Device Install - PCI\VEN_104C&DEV_8019&SUBSYS_8010104C&REV_00\3&61aaa01&0&38]
>>>  2005/02/13 22:06:28.109: Section start
```

 

 





