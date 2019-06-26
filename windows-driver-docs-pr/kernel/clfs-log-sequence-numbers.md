---
title: CLFS ログ シーケンス番号
description: CLFS ログ シーケンス番号
ms.assetid: 4637fa0c-2f19-4f0c-bf13-f4ccac2e7284
keywords:
- 一般的なログ ファイル システムの WDK カーネルでは、ログ シーケンス番号
- CLFS WDK カーネルでは、ログ シーケンス番号
- WDK CLFS のログ シーケンス番号
- Lsn の WDK CLFS
- 基本の Lsn WDK CLFS
- 最後の Lsn WDK CLFS
- 前の Lsn WDK CLFS
- 次への元に戻す Lsn WDK CLFS
- アクティブなストリーム部分 WDK CLFS
- アクティブな部分 WDK CLFS をストリーム配信します。
- ストリーム WDK CLFS
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41b8d8361c9d80e46bcd60c7aea093695c98a8f1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383374"
---
# <a name="clfs-log-sequence-numbers"></a>CLFS ログ シーケンス番号





Common Log File System (CLFS) では、指定されたストリーム内の各ログ レコードはログ シーケンス番号 (LSN) によって一意に識別します。 ストリームからレコードを書き込むときに戻る場合に備えて、そのレコードを識別する LSN。

厳密に増加するシーケンスが、特定のストリームのフォームの作成 Lsn。 つまり、指定されたストリーム内のログ レコードに割り当てられている LSN では、以前同じストリームに書き込まれたログ レコードに割り当てられている Lsn よりも大きいは常にします。 次の関数は、指定されたストリーム内のログ レコードの Lsn を比較するために使用できます。

[**ClfsLsnNull**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfslsnnull)

[**ClfsLsnEqual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfslsnequal)

[**ClfsLsnGreater**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfslsngreater)

[**ClfsLsnLess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfslsnless)

定数 CLFS\_LSN\_NULL と CLFS\_LSN\_無効なすべての有効な Lsn の下限と上限の境界。 任意の有効な LSN は CLFS 以上\_LSN\_NULL。 また、任意の有効な LSN は CLFS より厳密に小さい\_LSN\_が無効です。 注その CLFS\_LSN\_一方、NULL は有効な LSN では、CLFS\_LSN\_有効な LSN が無効です。 CLFS を比較するため、\_LSN\_を前の一覧に関数を使用して他の Lsn が無効です。

各ストリームでは、CLFS は追跡の 2 つの特殊な Lsn: ベース LSN と最後の LSN。 それぞれ個別のログ レコードには、2 つ特別な Lsn (以前の LSN と、元に戻す次の LSN) 関連するログ レコードのチェーンの作成に使用できるがあります。 次のセクションでは、これらの特殊な Lsn の詳細について説明します。

### <a name="base-lsn"></a>ベースの LSN

クライアントは、ストリームの最初のレコードを書き込む、CLFS は、その最初のレコードの lsn ベースの LSN を設定します。 ベースの LSN は、クライアントに変更しない限り変更されません。 ストリームのクライアントには、特定の時点でストリームする前にレコードが不要になった、ときに呼び出すことによってベースの LSN を更新できる[ **ClfsAdvanceLogBase** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfsadvancelogbase)または[ **ClfsWriteRestartArea**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfswriterestartarea)します。 たとえば、クライアントには、最初の 5 つのログ レコードが不要になった場合、は、6 番目のレコードの LSN をベースの LSN を設定ができます。

### <a name="last-lsn"></a>最後の LSN

クライアントは、レコードをストリームに書き込み、CLFS は最後に書き込まれたレコードの LSN では常にように最後の LSN を調整します。 クライアントには、レコードが不要になった場合、ストリームで特定の時点以降後、最後の LSN を呼び出すことで更新できる[ **ClfsSetEndOfLog**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfssetendoflog)します。 たとえば、クライアントには、10 番目のレコードの後に書き込まれたすべてのレコードが不要になった、10 番目のレコードの LSN を最後の LSN を設定して、ストリームを切り捨てることができます。

### <a name="active-portion-of-a-stream"></a>ストリームのアクティブな部分

*アクティブな部分*ベースの LSN を指すレコードで始まるストリームの部分は、ストリームの最後の LSN を指すレコードで終わります。 次の図は、ベース LSN と最後の LSN がストリームのアクティブな部分を記述する方法を示します。

![clfs ストリームのアクティブな部分を示す図](images/clfsactivelog.gif)

**注**  ベース LSN またはアーカイブ末尾が指すレコードで、ストリームのアクティブな部分が開始されますストリームをアーカイブ末尾にある場合は、小さい方です。 アーカイブの詳細については、次を参照してください。[アーカイブの CLFS サポート](clfs-support-for-archiving.md)します。

 

### <a name="previous-lsn"></a>前の LSN

たとえば、2 つのアクティブなデータベース トランザクション (トランザクション A と B のトランザクション) は、同時に、同じストリームにレコードを書き込んでいます。 毎回トランザクション A レコードの書き込みに設定、レコードの前の LSN A. のトランザクションによって書き込まれる前のログ レコードの LSNログ レコードのトランザクション A に属している逆の順序で走査可能のチェーンを形成します。 CLFS を設定、以前の LSN がトランザクション A によって書き込まれた最初のログ レコードで、チェーンが終わる\_LSN\_が無効です。 同様に、トランザクション B では、書き込む各ログ レコードの前の LSN を設定してログ レコードのチェーンを作成します。

次の図の矢印は、前のログ レコードの LSN が特定のトランザクションに属しているチェーンの前のレコードを指す方法を示しています。

![lsn の前のポインターを示す図](images/clfsrecordchains.gif)

### <a name="undo-next-lsn"></a>次への元に戻す LSN

トランザクションし揮発性のメモリ内のデータ オブジェクトを 5 つの更新プログラム 4 番目と 5 番目の更新プログラムをロールバックし、6 番目の更新します。 ログ レコードを書き込む、トランザクション、更新プログラムとして、1、2、3、4, 5, 5'、4'、および 6。 1 ~ 5 のログ レコードには、1 ~ 5 の更新プログラムによって行われた変更について説明します。 更新プログラム 5 のロールバック中に行われた変更レコード 5' とレコード 4' には、update 4 のロールバック中に行われた変更がについて説明します。 最後に、6 のレコードには、更新プログラム 6 で加えられた変更について説明します。 なお、数字 1、2、3、4, 5, 5'、4'、および 6 は、ログ レコードの Lsnここで説明するログ レコードの名前を使用する数字だけです。

5' ログに記録され、4'、ロールバックを記述するは、補正のログ レコード (Clr) で呼び出されます。 トランザクション (トランザクションによって書き込まれたレコード) の間での先行する各 CLR の元に戻す次 LSN の設定の更新をロールバックだけがログ レコードの (元に戻す)。 この例では、5' のレコードの元に戻す次の LSN は、4、レコードの LSN と 4' のレコードの元に戻す次の LSN が 3 のレコードの LSN。

(もの Clr ではない) 通常のログ レコードがある、元に戻す次 Lsn の前に、トランザクションによって書き込まれたログ レコードに設定します。 通常、レコードの LSN を元に戻す次、前の LSN は、同じです。

これで、システム障害が発生したと仮定し、再起動の復旧中に、トランザクション全体を戻すロールバックする必要があります。 回復用コードは、6 のログ レコードを読み取ります。 6 レコード内のデータの場合、6 のレコードが通常のレコード (CLR ではない) であることを示します、更新プログラム 6 のため、回復用コードをロールバックします。 回復用コードは、6 のレコードの元に戻す次の LSN を検査し、レコード 4' を指しているを検索します。 レコード 4' 内のデータは、ため、回復用コードはロールバックしない更新プログラム 4'、CLR はことを示します。 代わりに、4' のレコードの元に戻す次の LSN を検査し、3 のレコードを指していることを検出します。 回復用コードをロールバックするための更新プログラム 3 でレコード 3 は、CLR ではありません。 更新プログラム 5 および 4 はロールバックされません復旧中に、既にロールバックされた通常の転送処理中にあるためです。 回復用コードが最後にロールバック 2 と 1 に更新します。

次の図の矢印は、元に戻す次の LSN が回復コードを使用している更新プログラムが既にロールバックされているレコードをスキップする機構を提供する方法について説明します。

![前の lsn と元に戻す次の lsn のポインターを示す図](images/clfsundonext.gif)

 

 




