---
title: CLFS ログ シーケンス番号
description: CLFS ログ シーケンス番号
ms.assetid: 4637fa0c-2f19-4f0c-bf13-f4ccac2e7284
keywords:
- WDK カーネル、ログシーケンス番号の共通ログファイルシステム
- CLFS WDK カーネル、ログシーケンス番号
- ログシーケンス番号 WDK CLFS
- LSNs WDK CLFS
- ベース LSNs WDK CLFS
- 最後の LSNs WDK CLFS
- 前の LSNs WDK CLFS
- 元に戻す-next LSNs WDK CLFS
- アクティブストリーム部分 WDK CLFS
- アクティブ部分の CLFS WDK のストリーム
- CLFS WDK のストリーム
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c75c08cd1cf0b278ad21e2677a0f6a770f942353
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828554"
---
# <a name="clfs-log-sequence-numbers"></a>CLFS ログ シーケンス番号





共通ログファイルシステム (CLFS) では、特定のストリーム内の各ログレコードは、ログシーケンス番号 (LSN) によって一意に識別されます。 ストリームにレコードを書き込むと、後で参照できるようにそのレコードを識別する LSN が返されます。

特定のストリームに対して作成された Lsn は、厳密に増加するシーケンスを形成します。 つまり、特定のストリームのログレコードに割り当てられた LSN は、その同じストリームに以前に書き込まれたログレコードに割り当てられた LSN よりも常に大きくなります。 特定のストリーム内のログレコードの Lsn を比較するには、次の関数を使用できます。

[**ClfsLsnNull**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfslsnnull)

[**ClfsLsnEqual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfslsnequal)

[**ClfsLsnGreater**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfslsngreater)

[**ClfsLsnLess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfslsnless)

定数 CLFS\_LSN\_NULL および CLFS\_LSN\_INVALID は、すべての有効な lsn の下限と上限です。 有効な LSN が CLFS\_LSN\_NULL 以上です。 また、有効な LSN は、厳密には CLFS\_LSN\_無効です。 CLFS\_LSN\_NULL は有効な LSN であるのに対し、CLFS\_LSN\_INVALID は有効な LSN ではないことに注意してください。 それでも、前の一覧の関数を使用すると、CLFS\_LSN\_INVALID と他の LSN を比較できます。

各ストリームについて、CLFS は2つの特別な lsn (ベース LSN と最後の LSN) を追跡します。 また、個々のログレコードには、関連するログレコードのチェーンを作成するために使用できる2つの特別な lsn (前の LSN と元に戻す LSN) があります。 以下のセクションでは、これらの特別な Lsn について詳しく説明します。

### <a name="base-lsn"></a>ベース LSN

クライアントがストリームの最初のレコードを書き込むときに、CLFS は、ベース LSN を最初のレコードの LSN に設定します。 ベース LSN は、クライアントによって変更されるまで変更されません。 ストリームのクライアントがストリームの特定の時点より前のレコードを必要としなくなった場合、 [**ClfsAdvanceLogBase**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsadvancelogbase)または[**ClfsWriteRestartArea**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfswriterestartarea)を呼び出すことによってベース LSN を更新できます。 たとえば、クライアントが最初の5つのログレコードを必要としなくなった場合、ベース LSN を6番目のレコードの LSN に設定できます。

### <a name="last-lsn"></a>最後の LSN

クライアントがレコードをストリームに書き込むと、CLFS は最後の LSN を調整して、書き込まれた最後のレコードの LSN になるようにします。 ストリーム内の特定の位置より後にクライアントがレコードを必要としなくなった場合、 [**Clfssetendoflog**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfssetendoflog)を呼び出して最後の LSN を更新できます。 たとえば、クライアントが10番目のレコードの後に記述されたレコードを必要としなくなった場合、最後の LSN を10番目のレコードの LSN に設定することにより、ストリームを切り捨てることができます。

### <a name="active-portion-of-a-stream"></a>ストリームのアクティブな部分

ストリームの*アクティブな部分*は、ストリームのうち、ベース lsn が指すレコードで始まり、最後の lsn が指すレコードで終わる部分です。 次の図は、ベース LSN と最後の LSN がストリームのアクティブな部分をどのように表しているかを示しています。

![clfs ストリームのアクティブな部分を示す図](images/clfsactivelog.gif)

**メモ**   ストリームにアーカイブ末尾がある場合、ストリームのアクティブな部分は、ベース LSN または archive tail が指すレコードから開始されます。 アーカイブの詳細については、「 [CLFS Support For アーカイブ](clfs-support-for-archiving.md)」を参照してください。

 

### <a name="previous-lsn"></a>前の LSN

2つのアクティブなデータベーストランザクション (トランザクション A とトランザクション B) が同時に同じストリームにレコードを書き込んでいるとします。 トランザクション A がレコードを書き込むたびに、レコードの前の LSN がトランザクション A によって書き込まれた前のログレコードの LSN に設定されます。これは、逆の順序で走査できるトランザクション A に属するログレコードのチェーンを形成します。 このチェーンは、トランザクション A によって書き込まれた最初のログレコードで終了します。これには、前の LSN が CLFS に設定されていて、\_LSN が無効\_。 同様に、トランザクション B は、書き込まれる各ログレコードの前の LSN を設定することによって、独自のログレコードのチェーンを作成します。

次の図の矢印は、ログレコードの前の LSN が、特定のトランザクションに属するチェーン内の前のレコードを指していることを示しています。

![前の lsn ポインターを示す図](images/clfsrecordchains.gif)

### <a name="undo-next-lsn"></a>元に戻す-次の LSN

トランザクションが揮発性メモリ内のデータオブジェクトに対して5つの更新を行い、4番目と5番目の更新プログラムをロールバックした後、6番目の更新を行うとします。 トランザクションによって更新が行われると、ログレコード1、2、3、4、5、5、4、および6が書き込まれます。 ログレコード 1 ~ 5 は、update 1 から5によって行われた変更について説明します。 レコード 5 ' は、更新プログラム5のロールバック中に行われた変更を示し、レコード 4 ' は、更新プログラム4のロールバック中に行われた変更について説明します。 最後に、レコード6によって更新プログラム6によって行われた変更が説明されています。 数字1、2、3、4、5、5、4、および6は、ログレコードの Lsn ではないことに注意してください。この説明のために、ログレコードに名前を付けて使用するのは数字のみです。

ロールバックを説明するログレコード 5 ' と 4 ' は、補正ログレコード (CLRs) と呼ばれます。 トランザクションでは、更新がロールバック (元に戻す) されたばかりのログレコードの (トランザクションによって書き込まれたレコードの中から) 各 CLR の復元後の LSN を設定します。 この例では、レコード5の [元に戻す] の LSN はレコード4の LSN で、レコード4の [元に戻す] の lsn はレコード3の LSN です。

通常のログレコード (CLRs 以外のレコード) では、元に戻す次の Lsn が、トランザクションによって書き込まれた前のログレコードに設定されます。 つまり、通常のレコードの場合、元に戻す LSN と前の LSN は同じです。

ここで、システム障害が発生し、復旧の再開中にトランザクション全体をロールバックする必要があるとします。 復旧コードでは、ログレコード6が読み取られます。 レコード6のデータは、レコード6が (CLR ではなく) 通常のレコードであることを示しているので、復旧コードは update 6 をロールバックします。 次に、復旧コードは、レコード6の元に戻す LSN を調べ、レコード4を指していることを検出します。 レコード4のデータは、それが CLR であることを示しているので、復旧コードは update 4 をロールバックしません。 代わりに、レコード4の undo-next LSN を調べ、レコード3を指していることを検出します。 レコード3は CLR ではないため、復旧コードによって update 3 がロールバックされます。 更新プログラム5および4は、通常の転送処理中にロールバックされたため、復旧中にロールバックされません。 最後に、復旧コードによって更新プログラム2と1がロールバックされます。

次の図の矢印は、復旧コードが、既にロールバックされている更新プログラムがあるレコードをスキップするために使用できるメカニズムを示しています。

![前の lsn と undo-next lsn ポインターを示す図](images/clfsundonext.gif)

 

 




