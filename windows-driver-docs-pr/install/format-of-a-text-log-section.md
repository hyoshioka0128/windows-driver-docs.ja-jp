---
title: テキスト ログ セクションの書式
description: テキスト ログ セクションの書式
ms.assetid: e0f7227c-6cd8-4c66-a38b-104f222847bc
keywords:
- セクションでは WDK SetupAPI ログ記録
- WDK SetupAPI ログ出力を書式設定します。
- テキスト ログの WDK SetupAPI、セクション
- SetupAPI WDK Windows Vista では、ログのセクションではテキストをログ記録
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5de5987659e98dcc817d89d99a4eca1d9cff770f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377062"
---
# <a name="format-of-a-text-log-section"></a>テキスト ログ セクションの書式


A*テキスト ログ セクション*セクション ヘッダー セクションに表示される、一連のセクションの操作と、セクションを閉じるセクション フッターに適用するログ エントリを含むセクション本文が含まれます。 セクションに記述するのと同じ順序でのセクションでは、セクションのエントリが表示されます。

テキスト ログのセクションの次の例では、一般的なセクション、斜体のフォント スタイルのフィールド セクションに固有のテキストのプレース ホルダーでは、残りのテキストが太字のフォント スタイルでは、SetupAPI によって提供される一般テキストの一般的な形式を示します。 最初の 2 つのログ エントリは、セクションの見出しを構成し、最後の 2 つのログ エントリは、セクション フッターを構成します。

```cpp
>>>  [section_title - instance_identifer]
>>> time_stamp Section start
 section body log entry
 section body log entry
 section body log entry
<<<  [time_stamp: Section end]
<<<  [Exit Status(status_value)]
```

ログに記録されるセクション本文エントリは、ログが設定されているイベントのレベルと、ログを有効になっているカテゴリ レベルによって異なります。 これらの設定の詳細については、次を参照してください。 [SetupAPI ログのレジストリ設定](setupapi-logging-registry-settings.md)します。

次は、プラグ アンド プレイ (PnP) マネージャーが PCI デバイスのインストールを要請するログ エントリを作成、テキスト ログ セクションの一般的な例です。 セクションの見出し、 *section_title*フィールドは「デバイスをインストールする」、 *instance_identifier*フィールドは、デバイスのインスタンス識別子"PCI\\VEN_104C & DEV_8019 SUBSYS_8010104 C & REV_00\\3 & 61aaa01 & 0 & 38 で、"および*time_stamp*フィールドが"2005/02/13 22:06:28.109:." フッター セクションで、 *status_value*フィールドは"0x00000000"および*time_stamp*フィールドが"2005/02/13 22:06:20.000:." この例では、最初次の 3 つのセクションの本文のログ エントリのみが含まれます。 この例では、イベント レベルが TXTLOG_DETAILS に設定されており、この例では有効にしていたすべてのカテゴリ レベル。

```cpp
>>>  [Device Install - PCI\VEN_104C&DEV_8019&SUBSYS_8010104C&REV_00\3&61aaa01&0&38]
>>>  2005/02/13 22:06:20.000: Section start
     ndv: Retrieving device info...
     ndv: Setting device parameters...
     ndv: Building driver list...
...  
...  additional section body log entries, which are not shown
...  
<<<  [2005/02/13 22:06:28.109: Section end]
<<<  [Exit Status(0x00000000)]
```

詳細については、コンテンツと形式のテキストのログ セクションでは、次を参照してください[テキスト ログ セクション ヘッダーの形式](format-of-a-text-log-section-header.md)、[ログ セクションのテキスト本文の形式](format-of-a-text-log-section-body.md)、と[テキスト ログのセクションの形式。フッター](format-of-a-text-log-section-footer.md)します。

 

 





