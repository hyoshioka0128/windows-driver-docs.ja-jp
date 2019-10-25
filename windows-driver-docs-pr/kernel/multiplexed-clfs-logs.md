---
title: 多重化された CLFS ログ
description: 多重化された CLFS ログ
ms.assetid: bbea9bdc-8bb8-4455-89c4-4735bad85ba0
keywords:
- WDK カーネル、多重化ログの共通ログファイルシステム
- CLFS WDK カーネル、多重化ログ
- 多重化ログ WDK CLFS
- 安定したストレージ WDK CLFS
- storage WDK CLFS
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 087a91aef6b98a04517bc33a1506d569c7798a86
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827824"
---
# <a name="multiplexed-clfs-logs"></a>多重化された CLFS ログ





多重化された*ログ*は、複数のストリームに対して安定したストレージとして機能します。 *専用ログ*は、1つのストリームに対して安定したストレージとして機能します。 このトピックでは、多重化ログについて説明します。 専用ログの詳細については、[専用の CLFS ログ](dedicated-clfs-logs.md)を参照してください。

多重化されたログの各ストリームは、ストリームがログ全体であるという錯覚をクライアントに提供します。 このコンテキストのクライアントは、ドライバー、スレッド、または、共通ログファイルシステム (CLFS) ログへの書き込みと読み取りを行う他のソフトウェアの単位です。 1つのストリームに複数のクライアントを含めることができます。 各クライアントには、ストリームの開いているインスタンスを表す独自の[**ログ\_ファイル\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_object)構造があります。

2つのストリームを含む多重化されたログがあり、それぞれに1つのクライアントがある場合を考えてみます。 ログ、ストリーム、およびクライアントのマーシャリング領域を作成するには、次の手順に従います。

1.  クライアント1に代わって、 [**ClfsCreateLogFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfscreatelogfile)を呼び出して、**ログ\_ファイル\_オブジェクト**構造へのポインターを取得します。 *PuszLogFileName*パラメーターに "log:&lt;ログ名&gt;::&lt;ストリーム名&gt;" という形式の文字列を設定します。ここで &lt;ログ名&gt; は基になるファイルシステム上の有効なパスで、&lt;ストリーム名&gt; はです。クライアント1によって使用されるストリームに対して指定した名前。 たとえば、 *puszLogFileName*を "log: c:\\ClfsLogs\\myLog:: Stream1" に設定できます。 この場合、CLFS は myLog:\\ClfsLogs ディレクトリに基本ログファイルを作成し、Stream1 はクライアント1で使用されるストリームの名前になります。

    **メモ** これは、CLFS が専用ログと多重ログのどちらを作成するかを決定する、 *puszLogFileName*で渡される文字列の形式です。 文字列に2つのコロンがある場合 (::)パス名の後に、CLFS は多重化されたログを作成します。



2.  クライアント2に代わって、 [**ClfsCreateLogFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfscreatelogfile)を呼び出して、**ログ\_ファイル\_オブジェクト**構造へのポインターを取得します。 *PuszLogFileName*パラメーターに "log:&lt;ログ名&gt;::&lt;ストリーム名&gt;" という形式の文字列を設定します。ここで &lt;ログ名&gt; は、クライアント1で使用したのと同じパス名です。、および &lt;ストリーム名&gt; は、クライアント2によって使用されるストリームに提供するために選択した名前です。 たとえば、 *puszLogFileName*を "log: c:\\ClfsLogs\\myLog:: Stream2" に設定できます。

3.  ログレコードを保持する安定したストレージにコンテナー (連続した物理エクステント) を作成するには、 **ClfsCreateLogFile**から取得した**ログ\_ファイル\_オブジェクト**ポインターのいずれかを[**clfsaddlogcontainer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsaddlogcontainer)に渡します。 *Pcbcontainer*パラメーターを設定して、コンテナーのサイズを指定します (1 mb の倍数に切り上げられます)。 *PuszContainerPath*パラメーターを設定して、コンテナーのパス名を指定します。 パス名には、絶対パスまたはベースログファイルを含むディレクトリを基準とした相対パスを指定できます。

    **Clfsaddlogcontainer**を再度呼び出すことで、ログ用に追加のコンテナーを作成できます。 特定のログのすべてのコンテナーが同じサイズであることに注意してください。 **Clfsaddlogcontainer**を何度か呼び出す代わりに、 [**ClfsAddLogContainerSet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsaddlogcontainerset)を呼び出して複数のコンテナーを同時に作成することもできます。 コンテナーのセットは、クライアント1とクライアント2の両方によって書き込まれたログレコードの安定したストレージとして機能することに注意してください。

4.  クライアント1に代わって取得した**ログ\_ファイル\_オブジェクト**ポインターを[**ClfsCreateMarshallingArea**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfscreatemarshallingarea)に渡して、クライアント1がログレコードの読み取りと書き込みに使用できるマーシャリング領域へのポインターを取得します。 *Cbmarshalがバッファー*パラメーターを設定して、マーシャリング領域が使用するログ i/o ブロックのサイズを指定します。 他にもいくつかのパラメーターを使用して、マーシャリング領域のさまざまなプロパティを設定できます。

    クライアント1に追加のマーシャリング領域が必要な場合は、クライアント1が必要とする追加のマーシャリング領域ごとに、同じ**ログ\_ファイル\_オブジェクト**ポインターを再度**ClfsCreateMarshallingArea**に渡します。

5.  クライアント2に代わって取得した**ログ\_ファイル\_オブジェクト**ポインターを**ClfsCreateMarshallingArea**に渡して、クライアント2がログレコードの読み取りと書き込みに使用できるマーシャリング領域を取得します。 *Cbmarshalがバッファー*パラメーターを設定して、マーシャリング領域が使用するログ i/o ブロックのサイズを指定します。

    **メモ** 他にもいくつかのパラメーターを使用して、マーシャリング領域のさまざまなプロパティを設定できます。




クライアント2に追加のマーシャリング領域が必要な場合は、クライアント2が必要とする追加のマーシャリング領域ごとに、同じ**ログ\_ファイル\_オブジェクト**ポインターを再度**ClfsCreateMarshallingArea**に渡します。


クライアント1と2にはそれぞれ、**ログ\_ファイル\_オブジェクト**と1つ以上のマーシャリング領域があるので、次の関数を呼び出すことによって、それぞれのストリームにレコードを書き込むことができます (それらのストリームに関連付けられているマーシャリング領域によって)。

[**ClfsReserveAndAppendLog**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsreserveandappendlog)

[**ClfsReserveAndAppendLogAligned**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsreserveandappendlogaligned)

[**ClfsWriteRestartArea**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfswriterestartarea)

クライアント1および2によって書き込まれたすべてのログレコードは、同じログに記録されます。つまり、安定したストレージ上の同じ物理コンテナーのセットに対して行います。 CLFS は、2つのクライアントによって書き込まれたログレコードを多重化し、各ストリームに属しているレコードを追跡します。

クライアント1がレコードをストリームに書き込むと、レコードを識別するログシーケンス番号 (Lsn) の増加したシーケンスが返されます。 同様に、クライアント2は独自の Lsn のシーケンスを取得します。 特定のストリームに属する Lsn を比較して、対応するレコードが書き込まれた順序を判断できます。 ただし、あるストリームに属する LSN を別のストリームに属する LSN と比較することはできません。

CLFS は、すべてのストリームのベース LSN と最後の LSN を保持します。これには、多重化されたログを共有するストリームも含まれます。 各ストリームには、ベース LSN が指すレコードで始まり、最後の LSN が指すレコードで終わるアクティブな部分があります。 安定したストレージ上の多重化されたログ内のコンテナーは、すべてのログのストリームのベース Lsn が、そのコンテナーに格納されているレコードよりも高度なものになるまでリサイクルできないことに注意してください。








