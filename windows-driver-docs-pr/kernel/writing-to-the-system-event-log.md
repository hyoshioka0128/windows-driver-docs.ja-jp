---
title: システム イベント ログへの書き込み
description: システム イベント ログへの書き込み
ms.assetid: 19be8bb4-8736-4d1a-92e5-b63a5f04e254
keywords:
- NTSTATUS 値 WDK カーネル
- ダンプ データ WDK カーネル
- 定義済みのエラー コードの WDK カーネル
- システム イベント ログの WDK カーネル
- プロパティ シートの WDK エラー
- イベント ビューアーの WDK カーネル
- サンプルのログ エントリのプロパティ シートの WDK カーネル
- ログ エントリの WDK カーネル
- WDK エラー ログのエントリ
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0b61cd95a273450f777a86a71bd89d7fb4d63e7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374102"
---
# <a name="writing-to-the-system-event-log"></a>システム イベント ログへの書き込み





エラーは、その NTSTATUS 値によって指定されます。 システム、ドライバーで使用できる特定の NTSTATUS 値事前に定義し、ドライバー開発者がその他のエラーを定義できます。 エラーのログ記録するときに特定の NTSTATUS 値のみを使用できることに注意してください。

エラーのログ記録するときに使用できる各の NTSTATUS 値では、関連付けられているエラー メッセージがあります。 たとえば、パラレル ポート ドライバーは PAR NTSTATUS 値を使用\_割り込み\_ハードウェアを表す競合は"Interrupt 競合 %1 が検出されました"メッセージ テキストとの競合を中断します。

イベント ビューアーでのメッセージ テキストが表示されます、**説明**ログ エントリのプロパティ シートのテキスト ボックス。 メッセージのテキスト文字列には、「1」が含まれている、イベント ビューアーにより、エントリを記録するデバイスの名前を持つ置き換えます。 メッセージ テキストでは、"%2"、"%3"のフォームの追加のパラメーターを含めることができにすることができます。 ドライバーは、エラーを記録、ときに、これらのパラメーターの文字列値を提供できます。 これらの文字列値と呼ばれる*挿入文字列*します。 イベント ビューアーを自動的に挿入にパーセント値の代わりにします。

ドライバーと呼ばれる、ログ エントリのバイナリ データを含めることができますも*データ ダンプ*します。 イベント ビューアーのダンプ データを表示する、**データ**ログ エントリのプロパティ シートのテキスト ボックス。

使用できますログ エントリのプロパティ シートをエントリをダブルクリックすると、イベント ビューアー。 次のスクリーン ショットは、サンプル ログ エントリのプロパティ シートを示しています。

![イベントのプロパティ シートのスクリーン ショット](images/event-properties.png)

ドライバーを使用して、 [ **IoAllocateErrorLogEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateerrorlogentry)ルーチンをエラー ログのエントリを割り当てます。 ログ エントリは、可変長で構成されている[ **IO\_エラー\_ログ\_パケット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_error_log_packet)挿入文字列に続くヘッダー。

次の図はメモリ内のエラー ログのエントリのレイアウトを示します。

![メモリ内のエラー ログ パケットのレイアウトを示す図 ](images/errorlogentry.png)

**ErrorCode**のメンバー **IO\_エラー\_ログ\_パケット**エラーの NTSTATUS 値を指定します。 **DumpData**メンバーが、ダンプのデータのログ エントリを指定します。 **DumpData**でサイズが指定された、可変サイズの配列、 **DumpDataSize**メンバー。 ドライバーでは、最初の挿入文字列の先頭を指定する、 **StringOffset**メンバー、および内の文字列の数、 **NumberOfStrings**メンバー。 各挿入文字列自体は、null で終わる Unicode 文字列です。

使用して、エラー ログにエントリを書き込みますが、ドライバーは、割り当てられているエラーのログ エントリによって記入と[ **IoWriteErrorLogEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iowriteerrorlogentry)します。 **IoWriteErrorLogEntry**自動的にログ エントリに割り当てられたメモリを解放します。 ドライバーを使用できる[ **IoFreeErrorLogEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iofreeerrorlogentry)をすべての未使用のログ エントリを解放します。

定義済みのエラー コード (フォームの IO の\_ERR\_*XXX*) と Windows Driver Kit (WDK) に含まれている ntiologc.h ヘッダー ファイルで定義されます。 各エラー コードに関連付けられたエラー メッセージは、エラー コードの宣言の横にある、ntiologc.h のコメントにあります。 定義済みのエラー コードを使用するには、ドライバーは、関連するエラー メッセージのソースとして iologmsg.dll、システム ファイルを登録する必要があります。 詳細については、次を参照してください。[エラー メッセージのソースとして登録する](registering-as-a-source-of-error-messages.md)します。

ドライバーは、独自のカスタム エラー型を定義することも、関連するエラー メッセージ。 詳細については、次を参照してください。[カスタム エラーの種類を定義する](defining-custom-error-types.md)します。

 

 




