---
title: システム イベント ログへの書き込み
description: システム イベント ログへの書き込み
ms.assetid: 19be8bb4-8736-4d1a-92e5-b63a5f04e254
keywords:
- NTSTATUS 値 WDK カーネル
- データのダンプ WDK カーネル
- 事前定義されたエラーコード WDK カーネル
- システムイベントログの WDK カーネル
- プロパティシートの WDK エラー
- WDK カーネルのイベントビューアー
- サンプルログエントリのプロパティシート WDK カーネル
- ログエントリ WDK カーネル
- エントリ WDK エラーログ
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1428818ba060d04082400693edd355cdac9ddf1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835545"
---
# <a name="writing-to-the-system-event-log"></a>システム イベント ログへの書き込み





エラーは、NTSTATUS 値によって指定されます。 システム事前は、ドライバーで使用できる特定の NTSTATUS 値を指定します。ドライバーの作成者は、追加のエラーを定義できます。 エラーをログに記録するときに使用できるのは、特定の NTSTATUS 値のみであることに注意してください。

エラーをログに記録するときに使用できる各 NTSTATUS 値には、関連するエラーメッセージがあります。 たとえば、パラレルポートドライバーは、NTSTATUS 値 PAR\_割り込み\_競合を使用して、ハードウェアの割り込みの競合を表し、"%1 の割り込みの競合が検出されました" というメッセージテキストを表示します。

イベントビューアーは、ログエントリのプロパティシートの **[説明]** ボックスにメッセージテキストを表示します。 メッセージテキスト文字列に "%1" が含まれている場合、イベントビューアーは、エントリを記録したデバイスの名前に置き換えます。 メッセージテキストには、"%2"、"%3" などの形式の追加パラメーターを含めることができます。 ドライバーは、エラーをログに記録するときに、これらのパラメーターの文字列値を提供できます。 これらの文字列値は、*挿入文字列*と呼ばれます。 イベントビューアーによって、パーセント値の代わりに自動的に挿入されます。

ドライバーは、*ダンプデータ*と呼ばれるログエントリにバイナリデータを含めることもできます。 イベントビューアーは、ログエントリのプロパティシートの **[データ]** ボックスにダンプデータを表示します。

ログエントリのプロパティシートを表示するには、イベントビューアーのエントリをダブルクリックします。 次のスクリーンショットは、サンプルログエントリのプロパティシートを示しています。

![イベントプロパティシートのスクリーンショット](images/event-properties.png)

ドライバーは、 [**Ioallocateerrorlogentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateerrorlogentry)ルーチンを使用して、エラーログエントリを割り当てます。 ログエントリは、可変長[**IO\_エラー\_ログ\_パケット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_error_log_packet)ヘッダーの後に挿入文字列が続く形式で構成されます。

次の図は、メモリ内のエラーログエントリのレイアウトを示しています。

![メモリ内のエラーログパケットのレイアウトを示す図 ](images/errorlogentry.png)

**IO\_error\_LOG\_PACKET**の**ErrorCode**メンバーは、エラーの NTSTATUS 値を指定します。 **Dumpdata**メンバーは、ログエントリのすべてのダンプデータを指定します。 **Dumpdata**は、サイズが**dumpdata**メンバーによって指定された可変サイズの配列です。 ドライバーは、 **Stringoffset**メンバーを含む最初の挿入文字列の先頭と、 **numberofstrings**メンバー内の文字列の数を指定します。 各挿入文字列自体は、null で終わる Unicode 文字列です。

割り当てられたエラーログエントリがドライバーによって入力されると、 [**Iowriteerrorlogentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iowriteerrorlogentry)を使用して、エントリがエラーログに書き込まれます。 **Iowriteerrorlogentry**は、ログエントリに割り当てられたメモリを自動的に解放します。 ドライバーは[**IoFreeErrorLogEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeerrorlogentry)を使用して、未使用のログエントリを解放できます。

定義済みのエラーコード (フォーム IO\_ERR\_*XXX*) は、Windows Driver KIT (WDK) に含まれている ntiologc .h ヘッダーファイルで定義されています。 各エラーコードに関連付けられているエラーメッセージは、エラーコードの宣言の横にある ntiologc. h のコメントに記載されています。 定義済みのエラーコードを使用するには、ドライバーは、関連付けられたエラーメッセージのソースとして、システムファイル iologmsg .dll を登録する必要があります。 詳細については、「[エラーメッセージのソースとしての登録](registering-as-a-source-of-error-messages.md)」を参照してください。

ドライバーでは、独自のカスタムエラーの種類や関連するエラーメッセージを定義することもできます。 詳細については、「[カスタムエラーの種類の定義](defining-custom-error-types.md)」を参照してください。

 

 




