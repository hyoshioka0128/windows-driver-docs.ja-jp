---
title: 多重化された CLFS ログ
description: 多重化された CLFS ログ
ms.assetid: bbea9bdc-8bb8-4455-89c4-4735bad85ba0
keywords:
- 一般的なログ ファイル システムの WDK カーネル、多重化されたログ
- CLFS WDK カーネル、多重化されたログ
- WDK CLFS ログを多重化
- 安定したストレージ WDK CLFS
- 記憶域 WDK CLFS
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 139c31e579d9ef321025f9e7a962125d1c5acc4d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580980"
---
# <a name="multiplexed-clfs-logs"></a>多重化された CLFS ログ





A*ログを多重化*は複数のストリームの安定したストレージとして機能します。 A*専用ログ*は 1 つのストリームの安定したストレージとして機能します。 このトピックでは、多重化されたログについて説明します。 専用ログについては、次を参照してください。[専用 CLFS ログ](dedicated-clfs-logs.md)します。

多重化されたログの各ストリームでは、そのクライアント、ストリームは、ログ全体を錯覚を提供します。 このコンテキストで、クライアントとは、ドライバー、スレッド、または Common Log File System (CLFS) ログから読み取りし、書き込みするソフトウェアの他のいくつかの単位です。 いくつかのクライアントが 1 つのストリームのことができます。 各クライアントが、独自[**ログ\_ファイル\_オブジェクト**](https://msdn.microsoft.com/library/windows/hardware/ff554316)構造体は、ストリームのオープン インスタンスを表します。

多重化されたログを 2 つのストリームを持つ 1 つのクライアントがあり、いずれの場合を考えます。 次の手順を使用するには、ログ、ストリーム、および、クライアント領域をマーシャ リングを作成します。

1.  クライアント 1、に代わって呼び出す[ **ClfsCreateLogFile** ](https://msdn.microsoft.com/library/windows/hardware/ff540792)へのポインターを取得する、**ログ\_ファイル\_オブジェクト**構造体。 設定、 *puszLogFileName*パラメーター形式の文字列を"ログ:&lt;ログ名&gt;::&lt;ストリーム名&gt;"場所&lt;ログ名&gt;が有効なパスをファイル システムを基になると&lt;ストリーム名&gt;クライアント 1 が使用されるストリームを提供する、選択した名前を指定します。 たとえば、設定した*puszLogFileName*に"ログ: c:\\ClfsLogs\\myLog::Stream1"。 その場合は、CLFS は、c: ベースのログ ファイルの myLog.blf を作成、\\ClfsLogs のディレクトリと Stream1 には、クライアント 1 が使用するストリームの名前になります。

    **注**で渡された文字列の形式は*puszLogFileName* CLFS が専用または多重化されたログを作成するかどうかを決定します。 文字列に 2 つのコロン (:) がある場合パス名の後、CLFS ログを作成多重化されました。



2.  クライアント 2、に代わって呼び出す[ **ClfsCreateLogFile** ](https://msdn.microsoft.com/library/windows/hardware/ff540792)へのポインターを取得する、**ログ\_ファイル\_オブジェクト**構造体。 設定、 *puszLogFileName*パラメーター形式の文字列を"ログ:&lt;ログ名&gt;::&lt;ストリーム名&gt;"場所&lt;ログ名&gt;同じパス名にはクライアント 1 を使用した、&lt;ストリーム名&gt;2 クライアントによって使用されるストリームを提供する、選択した名前を指定します。 たとえば、設定した*puszLogFileName*に"ログ: c:\\ClfsLogs\\myLog::Stream2"。

3.  いずれかを渡す、**ログ\_ファイル\_オブジェクト**から取得したポインター **ClfsCreateLogFile**に[ **ClfsAddLogContainer**](https://msdn.microsoft.com/library/windows/hardware/ff540768)ログ レコードを保持する安定したストレージにコンテナー (物理的なエクステントの連続する) を作成します。 (これは切り上げられます 1 メガバイトの倍数に) コンテナーのサイズを設定して指定、 *pcbContainer*パラメーター。 設定、 *puszContainerPath*コンテナーのパス名を指定するパラメーター。 絶対パスまたは基本のログ ファイルを格納するディレクトリに対する相対パス名ができます。

    呼び出すことによって、ログの追加のコンテナーを作成する**ClfsAddLogContainer**もう一度です。 特定のログのすべてのコンテナーは同じサイズである必要がありますに注意してください。 呼び出す代わりとして**ClfsAddLogContainer**を複数回呼び出すことができます[ **ClfsAddLogContainerSet** ](https://msdn.microsoft.com/library/windows/hardware/ff540770)を同時に複数のコンテナーを作成します。 一連のコンテナーがクライアント 1 と 2 のクライアントの両方で書き込まれたログ レコードの安定したストレージとして使用することに注意してください。

4.  渡す、**ログ\_ファイル\_オブジェクト**1 にそのクライアントに代わって取得したポインター [ **ClfsCreateMarshallingArea** ](https://msdn.microsoft.com/library/windows/hardware/ff541520)へのポインターを取得する、領域をマーシャ リング クライアント 1 がログ レコードの読み書きに使用できます。 マーシャ リングの領域を設定して使用する I/O のログ ブロックのサイズを指定、 *cbMarshallingBuffer*パラメーター。 マーシャ リング領域のさまざまなプロパティを設定する際の他のいくつかのパラメーターがあります。

    クライアント 1 では、その他のマーシャ リング領域を必要とする場合は、同じを渡す**ログ\_ファイル\_オブジェクト**へのポインター **ClfsCreateMarshallingArea**ここでも、各マーシャ リングに対して 1 回領域クライアント 1 が必要があります。

5.  渡す、**ログ\_ファイル\_オブジェクト**に代わってクライアント 2 を取得したポインター **ClfsCreateMarshallingArea**マーシャ リング領域にそのクライアントを取得する 2 は、読み取りし、書き込みに使用できますログを記録します。 マーシャ リングの領域を設定して使用する I/O のログ ブロックのサイズを指定、 *cbMarshallingBuffer*パラメーター。

    **注**マーシャ リング領域のさまざまなプロパティを設定する際の他のいくつかのパラメーターがあります。




クライアント 2 では、その他のマーシャ リング領域を必要とする場合は、同じを渡す**ログ\_ファイル\_オブジェクト**へのポインター **ClfsCreateMarshallingArea**ここでも、各マーシャ リングに対して 1 回領域クライアント 2 が必要があります。


クライアント 1 と 2 が完了したので、**ログ\_ファイル\_オブジェクト**1 つまたは複数のマーシャ リング領域それぞれが書き込み可能なレコード (これらのストリームに関連付けられている領域のマーシャ リング) を使用して、独自のストリームで、次の関数を呼び出しています。

[**ClfsReserveAndAppendLog**](https://msdn.microsoft.com/library/windows/hardware/ff541723)

[**ClfsReserveAndAppendLogAligned**](https://msdn.microsoft.com/library/windows/hardware/ff541726)

[**ClfsWriteRestartArea**](https://msdn.microsoft.com/library/windows/hardware/ff541770)

すべてのログ 1 および 2 には、同じログ; クライアントによって書き込まれたレコード同じには、物理コンテナーの設定安定したストレージにします。 CLFS は、2 つのクライアントによって書き込まれたログ レコードを多重化し、各ストリームに属しているレコードの追跡します。

クライアント 1 では、そのストリームにレコードを書き込む、それらのレコードを識別するログ シーケンス番号 (Lsn) の増加するシーケンスで取得バックアップします。 同様に、クライアント 2 は、独自の Lsn の順序を取得します。 対応するレコードが書き込まれた順序を決定する特定のストリームに属している Lsn を比較できます。 ただし、1 つのストリームが属する LSN は、別のストリームが属する LSN を比較できません。

CLFS は、ベース LSN と多重化されたログを共有するストリームを含む、すべてのストリームの最後の LSN を維持します。 各ストリームは、アクティブな部分で、ベースの LSN を指すレコードで始まり、最後の LSN を指すレコードで終わるを持ちます。 安定したストレージに多重化されたログ内のコンテナーをログのストリームがそのコンテナーに格納されているレコードを超える高度なすべてのベース Lsn まで再利用することはできませんに注意してください。








