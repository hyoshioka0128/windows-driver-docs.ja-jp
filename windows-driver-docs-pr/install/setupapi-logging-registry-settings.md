---
title: SetupAPI のログ レジストリの設定
description: SetupAPI のログ レジストリの設定
ms.assetid: 24694bce-5941-479f-9e2d-f9c7577a4f6a
keywords:
- SetupAPI WDK Windows Vista では、レジストリ設定のログ記録
- レジストリの WDK SetupAPI ログ記録
- イベント レベルの WDK SetupAPI ログ
- イベント カテゴリの WDK SetupAPI ログ
- テキスト ログの WDK SetupAPI、レジストリ エントリ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9307a0b28bb4ed6b635e03ceabac500836299750
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348648"
---
# <a name="setupapi-logging-registry-settings"></a>SetupAPI のログ レジストリの設定


[SetupAPI](setupapi.md)ログ記録をサポート、グローバル*イベント レベル*とグローバル*イベント カテゴリ*テキスト ログに書き込まれる情報であるかどうかを制御します。 イベントのレベルは、テキスト ログに書き込まれる詳細レベルを制御し、イベント カテゴリのログ エントリが可能な操作の種類を決定します。 テキスト ログにログ エントリが書き込まれるログ エントリがあるイベント レベル以下の数値またはテキスト ログのイベントのグローバル レベルと等しい場合、およびテキスト ログのログ エントリのイベント カテゴリが有効になっている場合は、それ以外の場合、ログ エントリは、テキスト ログには書き込まれません。

イベント レベルを設定する方法については、次を参照してください。[テキスト ログのイベント レベルの設定](setting-the-event-level-for-a-text-log.md)します。

ログを有効になっているイベント カテゴリを設定する方法については、次を参照してください。[テキスト ログのイベント カテゴリを有効にする](enabling-event-categories-for-a-text-log.md)します。

既定では、SetupAPI のテキスト ログは % にあります*SystemRoot*%*\\Inf*ディレクトリ。 テキスト ログが保存されているディレクトリを変更する方法については、次を参照してください。[テキスト ログのディレクトリ パスを設定する](setting-the-directory-path-of-the-text-logs.md)します。

 

 





