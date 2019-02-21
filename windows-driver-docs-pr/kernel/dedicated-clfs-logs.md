---
title: 専用 CLFS ログ
description: 専用 CLFS ログ
ms.assetid: c6ca580c-b7f4-493a-8bd6-35d0aa932b1a
keywords:
- 一般的なログ ファイル システムの WDK カーネルでは、専用のログ
- CLFS WDK カーネルでは、専用のログ
- 専用ログ WDK CLFS
- 安定したストレージ WDK CLFS
- 記憶域 WDK CLFS
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 860735d2ae97d08a090a888b324079754b771257
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557610"
---
# <a name="dedicated-clfs-logs"></a>専用 CLFS ログ





Common Log File System (CLFS) ログは、いずれか専用または多重化します。 A*専用ログ*は 1 つのストリームの安定したストレージとして機能します。 A*ログを多重化*は複数のストリームの安定したストレージとして機能します。 このトピックでは、専用のログについて説明します。 多重化されたログについては、次を参照してください。 [CLFS ログの多重化](multiplexed-clfs-logs.md)します。

専用のログを作成するには、次の手順を実行します。

1.  呼び出す[ **ClfsCreateLogFile** ](https://msdn.microsoft.com/library/windows/hardware/ff540792)へのポインターを取得する、 [**ログ\_ファイル\_オブジェクト**](https://msdn.microsoft.com/library/windows/hardware/ff554316)構造体。 設定、 *puszLogFileName*パラメーター形式の文字列を"ログ:*&lt;ログ名&gt;*"場所*&lt;ログ名&gt;* は基になるファイル システムの有効なパスです。 例では、設定した場合の*puszLogFileName*に"ログ: c:\\ClfsLogs\\myLog"、c: で作成されるベースのログ ファイルの myLog.blf\\ClfsLogs ディレクトリ。 C:\\ClfsLogs ディレクトリは、後で、ログに追加するコンテナーの既定の場所としても機能します。

    **注**で渡された文字列の形式は*puszLogFileName* CLFS が専用または多重化されたログを作成するかどうかを決定します。 文字列に 2 つのコロン (:) がある場合ログ名の後、CLFS ログを作成多重化されました。 ここでは、この例では"ログ: c\\ClfsLogs\\myLog"CLFS は、専用のログを作成します。 は、二重のコロンがありません。




**ログ\_ファイル\_オブジェクト**によって返されたポインター **ClfsCreateLogFile**専用ログの 1 つとだけストリームのオープン インスタンスを表します。


2.  渡す、**ログ\_ファイル\_オブジェクト**から取得したポインター **ClfsCreateLogFile**に[ **ClfsAddLogContainer** ](https://msdn.microsoft.com/library/windows/hardware/ff540768)ログ レコードを保持する安定したストレージにコンテナー (物理的なエクステントの連続する) を作成します。 (これは切り上げられますは 512 の倍数に) コンテナーのサイズを設定して指定、 *pcbContainer*パラメーター。 設定、 *puszContainerPath*コンテナーのパス名を指定するパラメーター。 絶対パスまたは基本のログ ファイルを格納するディレクトリに対する相対パス名ができます。

    呼び出すことによって、ログの追加のコンテナーを作成する**ClfsAddLogContainer**もう一度です。 特定のログのすべてのコンテナーは同じサイズである必要がありますに注意してください。 呼び出す代わりとして**ClfsAddLogContainer**を複数回呼び出すことができます[ **ClfsAddLogContainerSet** ](https://msdn.microsoft.com/library/windows/hardware/ff540770)を同時に複数のコンテナーを作成します。

3.  渡す、**ログ\_ファイル\_オブジェクト**から取得したポインター **ClfsCreateLogFile**に[ **ClfsCreateMarshallingArea**](https://msdn.microsoft.com/library/windows/hardware/ff541520)をストリームにログ レコードの読み書きに使用できる、マーシャ リング領域へのポインターを取得します。 マーシャ リングの領域を設定して使用する I/O のログ ブロックのサイズを指定、 *cbMarshallingBuffer*パラメーター。 マーシャ リング領域のさまざまなプロパティを設定する際の他のいくつかのパラメーターがあります。

    その他のマーシャ リング領域が必要な場合は、同じを渡す**ログ\_ファイル\_オブジェクト**へのポインター **ClfsCreateMarshallingArea**ここでも、追加のマーシャ リング領域ごとに 1 回必要です。

ストリームと関連付けられている 1 つまたは複数のマーシャ リング領域をしたので、次の関数を呼び出すことによって領域をマーシャ リングにレコードを記述できます。

[**ClfsReserveAndAppendLog**](https://msdn.microsoft.com/library/windows/hardware/ff541723)

[**ClfsReserveAndAppendLogAligned**](https://msdn.microsoft.com/library/windows/hardware/ff541726)

[**ClfsWriteRestartArea**](https://msdn.microsoft.com/library/windows/hardware/ff541770)

レコードを作成するたびに戻るレコードを識別するログ シーケンス番号 (LSN)。 レコードに割り当てられている LSN は、レコードを書き込むことに関係なく使用領域をマーシャ リングされた、以前に書き込まれたレコードに割り当てられている LSN よりも大きいは常にします。








