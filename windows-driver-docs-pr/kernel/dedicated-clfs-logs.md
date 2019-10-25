---
title: 専用 CLFS ログ
description: 専用 CLFS ログ
ms.assetid: c6ca580c-b7f4-493a-8bd6-35d0aa932b1a
keywords:
- WDK カーネル、専用ログの共通ログファイルシステム
- CLFS WDK カーネル、専用ログ
- 専用ログ WDK CLFS
- 安定したストレージ WDK CLFS
- storage WDK CLFS
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: fffc480c3ae74313ccc05395f9543e9feb1515cc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836951"
---
# <a name="dedicated-clfs-logs"></a>専用 CLFS ログ





共通ログファイルシステム (CLFS) ログは、専用または多重化することができます。 *専用ログ*は、1つのストリームに対して安定したストレージとして機能します。 多重化された*ログ*は、複数のストリームに対して安定したストレージとして機能します。 このトピックでは、専用のログについて説明します。 多重化ログの詳細については、「[マルチプレクシング CLFS logs](multiplexed-clfs-logs.md)」を参照してください。

専用のログを作成するには、次の手順を実行します。

1.  [**ClfsCreateLogFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfscreatelogfile)を呼び出して、[**ログ\_ファイル\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_object)構造へのポインターを取得します。 *PuszLogFileName*パラメーターを "log: *&lt;log name&gt;* " という形式の文字列に設定します。ここで *&lt;ログ名&gt;* は、基になるファイルシステムの有効なパスです。 たとえば、 *puszLogFileName*を "log: c:\\clfslogs\\myLog" に設定した場合、基本ログファイル myLog は c:\\clfslogs ディレクトリに作成されます。 C:\\ClfsLogs ディレクトリは、後でログに追加するコンテナーの既定の場所としても機能します。

    **メモ** これは、CLFS が専用ログと多重ログのどちらを作成するかを決定する、 *puszLogFileName*で渡される文字列の形式です。 文字列に2つのコロンがある場合 (::)ログ名の後に CLFS は、多重化されたログを作成します。 ここで示す例では、"log: c\\ClfsLogs\\myLog" には2つのコロンがないため、CLFS は専用のログを作成します。




**ClfsCreateLogFile**によって返される**ログ\_ファイル\_オブジェクト**ポインターは、専用ログの1つの開いているインスタンスを表し、ストリームのみを表します。


2.  ログレコードを保持する安定したストレージにコンテナー (連続した物理エクステント) を作成するには、 **ClfsCreateLogFile**から取得した**ログ\_ファイル\_オブジェクト**ポインターを[**clfsaddlogcontainer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsaddlogcontainer)に渡します。 *Pcbcontainer*パラメーターを設定して、コンテナーのサイズを指定します (これは512キロバイトの倍数に切り上げられます)。 *PuszContainerPath*パラメーターを設定して、コンテナーのパス名を指定します。 パス名には、絶対パスまたはベースログファイルを含むディレクトリを基準とした相対パスを指定できます。

    **Clfsaddlogcontainer**を再度呼び出すことで、ログ用に追加のコンテナーを作成できます。 特定のログのすべてのコンテナーが同じサイズであることに注意してください。 **Clfsaddlogcontainer**を何度か呼び出す代わりに、 [**ClfsAddLogContainerSet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsaddlogcontainerset)を呼び出して複数のコンテナーを同時に作成することもできます。

3.  **ClfsCreateLogFile**から取得した**ログ\_ファイル\_オブジェクト**ポインターを[**ClfsCreateMarshallingArea**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfscreatemarshallingarea)に渡して、ストリームに対するログレコードの読み取りと書き込みに使用できるマーシャリング領域へのポインターを取得します。 *Cbmarshalがバッファー*パラメーターを設定して、マーシャリング領域が使用するログ i/o ブロックのサイズを指定します。 他にもいくつかのパラメーターを使用して、マーシャリング領域のさまざまなプロパティを設定できます。

    追加のマーシャリング領域が必要な場合は、必要な追加のマーシャリング領域ごとに、同じ**ログ\_ファイル\_オブジェクト**ポインターを再度**ClfsCreateMarshallingArea**に渡します。

これで、1つまたは複数のマーシャリング領域がストリームに関連付けられたので、次の関数を呼び出して、それらのマーシャリング領域にレコードを書き込むことができます。

[**ClfsReserveAndAppendLog**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsreserveandappendlog)

[**ClfsReserveAndAppendLogAligned**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsreserveandappendlogaligned)

[**ClfsWriteRestartArea**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfswriterestartarea)

レコードを作成するたびに、レコードを識別するログシーケンス番号 (LSN) が返されます。 レコードに割り当てられた LSN は、レコードの書き込みに使用されたマーシャリング領域に関係なく、常に、以前に書き込まれたレコードに割り当てられた LSN よりも大きくなります。








