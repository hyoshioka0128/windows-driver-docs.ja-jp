---
title: CLFS の安定した記憶域
description: CLFS の安定した記憶域
ms.assetid: d0ee4f22-9fba-47da-a9c9-eaf3a21feb36
keywords:
- 一般的なログ ファイル システムの WDK カーネル、安定したストレージ
- CLFS WDK カーネル、安定したストレージ
- 安定したストレージ WDK CLFS
- 記憶域 WDK CLFS
- WDK CLFS コンテナー
- WDK CLFS の論理的なコンテナー
- WDK CLFS の物理コンテナー
- ログの I/O WDK CLFS をブロックします。
- WDK CLFS をブロックします。
- ブロックは、WDK CLFS をオフセットします。
- WDK CLFS ログに記録します。
- 物理ログ WDK CLFS
- コンテナー識別子 WDK CLFS
- レコードのシーケンス番号の WDK CLFS
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1845d10b75f80205290b987b695c4dd17d32e691
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383341"
---
# <a name="clfs-stable-storage"></a>CLFS の安定した記憶域





レコードは、Common Log File System (CLFS) ストリームに書き込み、レコードは揮発性メモリ (マーシャ リング領域) のログ I/O ブロックに配置されます。 定期的に、CLFS フラッシュのログ ディスクなどのストレージを安定にマーシャ リング領域から I/O ブロックします。 安定したストレージ デバイスでは、コンテナーのそれぞれが、物理メディア上の連続する範囲の一連のログで構成されます。 ストリームの安定したストレージを形成するコンテナーのコレクションと呼ばれる、*ログ*、または*物理ログ*します。

次の図は、コンテナーを示しています。

![コンテナー、ブロック、およびレコードを示す図します。](images/clfscontainers.gif)

上記の図は、次の 3 つのログ I/O ブロックを保持するコンテナーを示しています。 最初のログ I/O ブロックには、3 つのレコードが含まれています、2 つ目には、5 つのレコードが含まれています。 および、3 番目には 2 つのレコードが含まれています。 図からわかるように、各ログの I/O ブロックの先頭は常に安定したストレージ メディア上のセクターの先頭に配置します。 安定したストレージにログの I/O ブロック サイズと異なることに注意してください。

CLFS では、次の 3 つの数値のセットを使用して、ログ レコードを見つけます。

-   *コンテナー識別子*レコードを保持するコンテナーを識別します。

-   *ブロック オフセット*レコードを保持するログの I/O ブロックの先頭のコンテナー内のバイト オフセットを示します。

-   *シーケンスを記録*数は、ログ I/O ブロック内でレコードを識別します。

CLFS ログ レコードのログ シーケンス番号 (LSN) が実際にこれら 3 つの情報を保持します。 コンテナーの識別子、ブロックのオフセット、およびレコードのシーケンス番号。 ただし、クライアントのログに指定された Lsn が含まれている*論理のコンテナー識別子*CLFS は、安定したストレージのレコードにアクセスする前に物理コンテナー識別子をマップする必要があります。

CLFS は、論理的なコンテナーの識別子を使用して、クライアント ログに記録するビューが書き込まれているときに、実際には、コンテナーの継続的なシーケンスに物理コンテナーがリサイクルされています。

3 つのコンテナーのログと、1 つのクライアントが CLFS レコードをログに書き込むとします。 次のシナリオでは、コンテナーが再利用する可能性がありますの方法を示します。

1.  クライアントは、次の 3 つのすべてのコンテナーに格納するには、十分なログ レコードを書き込みます。

2.  クライアント ログを基本に設定します (呼び出して[ **ClfsAdvanceLogBase** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfsadvancelogbase)または[ **ClfsWriteRestartArea**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfswriterestartarea)) コンテナー内のレコードのいずれかに。2 です。 行うと、クライアントはコンテナー 1 内のレコードを必要がなくなったこと示します。

3.  クライアントは、別のレコードをログに書き込むし、新規に書き込まれるレコードの LSN を取得します。 その LSN で論理的なコンテナーの識別子には 4 です。 レコードは安定ストレージにフラッシュされる、物理コンテナー 1 に、クライアントが 4 の論理コンテナーに表示されるレコードは変わります。

次の図は、シナリオを示しています安定したストレージ上の物理コンテナーに論理的なコンテナーのクライアントのシーケンスをマップする方法を示します。

![論理的および物理的なコンテナーを示す図](images/clfslogicalcontainers.gif)

論理的なコンテナーの識別子、ブロックのオフセット、およびレコードのシーケンス番号は、方法、特定の Lsn をストリーム常にフォームを厳密に増加するシーケンスで、LSN に格納されます。 つまり、ストリームに書き込まれたログ レコードの LSN を (論理コンテナー識別子) を持つでは、以前同じストリームに書き込まれたログ レコードの Lsn よりも大きいは常にします。 Lsn は、次に、2 つの目的を果たします。レコードの識別子の順序付けされた一連のストリームのクライアントを与える 1)、し、2)、レコードを安定したストレージの場所 CLFS を提供します。

レコードの LSN を指定するには、次の関数を呼び出すことでの論理コンテナーの識別子、ブロックのオフセット、およびレコードのシーケンス番号を抽出できます。

[**ClfsLsnContainer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfslsncontainer)

[**ClfsLsnBlockOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfslsnblockoffset)

[**ClfsLsnRecordSequence**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfslsnrecordsequence)

論理的なコンテナーの識別子が、32 ビット数値 2 ^32 の可能な論理的なコンテナーの識別子、およびそれらが 0 xffffffff を範囲 0x0 内にあります。 ストリームが最大で 2 ^32 の論理コンテナーです。

ブロックのオフセットが、LSN の 23 ビットで格納されているが、 **ClfsLsnBlockOffset**安定したストレージ メディアのセクター サイズに固定する 32 ビットの数値を返します。 ブロックのオフセットは 512 の倍数では常にします。 また、ブロックのオフセットは、安定したストレージ メディアのセクター サイズに揃えられます。 たとえば、セクター サイズが 1024 バイトの場合は、ブロックのオフセット。 1024 の倍数になります。

2 があるために、レコードのシーケンス番号は 9 ビットの数値では、^9 (512) 可能なレコードのシーケンス番号、およびそれらが範囲 0x1FF を通じて 0x0。 ログの I/O ブロックには、最大で 512 レコードをことができます。

 

 




